---
date: 2022-04-06 21:06:52
layout: post
title: Zabbix 5 - Instalação no Ubuntu Server
subtitle: ""
description: Instalação de um servidor Zabbix no Ubuntu
image: https://res.cloudinary.com/k4bv734/image/upload/v1649289936/blog/zabbix_i5azuy.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1649289936/blog/zabbix_optimized_pfmyho.jpg
category: tutorial
tags:
  - zabbix
  - linux
  - ubuntu
  - monitoramento
  - logs
author: brunocosta
paginate: false
---
Neste tutorial utilizaremos:
* Ubuntu 20.04.3
* Zabbix 5.4.0
* MySQL 8.0
* PHP 7.4
* GOLANG
* IP 192.168.0.100 (Recomendo que configure IP fixo em seu servidor)

Primeiro verifique atualizações do sistema. Veja os comando abaixo:  
Atualizando a lista de pacotes e programas:  
```
sudo apt-get update
```
 
Atualiza o sistema, realiza o download e instala atualizações de pacotes e dos programas do servidor:  
```
sudo apt-get upgrade
```

## Instalando e preparando o banco de dados

Instale o serviço de banco de dados *MySQL*:  
```
sudo apt-get install mysql-server mysql-client
```

Após a instalação, acesse a linha de comando de serviço *MySQL*:  
```
mysql -u root -p
```

Crie um banco de dados chamado *zabbix* :  
```
CREATE DATABASE zabbix CHARACTER SET UTF8 COLLATE UTF8_BIN;
```

Crie um usuário de banco de dados chamado *zabbix*. Note que estou definindo uma senha a esse usuário como *zabbix123* :  
```
CREATE USER 'zabbix'@'%' IDENTIFIED BY 'zabbix123';
```

Dê a esse usuário chamado *zabbix* permissões sobre o banco de dados chamado *zabbix* :  
```
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'%';
```

Dê o comando abaixo para sair do CLI MySQL:
```
quit;
```

A partir de agora, vamos fazer o download o pacote de instalação *Zabbix*.
Para melhor organização, primeiro crie um novo diretório:  
```
mkdir /downloads
```

Após a criação, acesse esse diretório pré-criado:  
```
cd /downloads
```

Agora sim iremos fazer o download do *Zabbix*. Aqui iremos baixar a última versão estável disponível na data de publicação deste post (5.4):  
```
sudo wget https://cdn.zabbix.com/zabbix/sources/stable/5.4/zabbix-5.4.0.tar.gz
```

Descompactando o pacote baixado:  
```
tar -zxvf zabbix-5.4.0.tar.gz
```

Acessando diretório após descompactação:  
```
cd zabbix-5.4.0/database/mysql/
```

Importação do modelo de banco de dados. Um comando por vez!  
```
mysql -u zabbix -p zabbix < schema.sql
mysql -u zabbix -p zabbix < images.sql
mysql -u zabbix -p zabbix < data.sql
```

Pronto! Finalizada a instalação do banco de dados *Zabbix*.

## Instalando o servidor web

Instale o servidor web *Apache* e todos os pacotes necessários:  
```
sudo apt-get install apache2 php libapache2-mod-php php-cli php-mysql php-mbstring php-gd php-xml php-bcmath php-ldap mlocate
```

Dê o comando abaixo:  
```
sudo updatedb
```

Logo após, encontre a localização do arquivo *php.ini* no seu sistema:  
```
locate php.ini
```

Após o comando acima, será apresentado o local onde se encontra o *php.ini* .
Edite o arquivo *php.ini* . Aqui iremos utilizar o *Vi*, porém fique a vontade pra utilizar o editor de textos de sua preferência:  
```
sudo vi /etc/php/7.4/apache2/php.ini
```

No *php.ini* , defina os seguintes itens conforme abaixo:  
```
max_execution_time = 300
memory_limit = 256M
post_max_size = 32M
max_input_time = 300
date.timezone = America/Sao_Paulo
```
**NOTA:** Em *date.timezone* edite conforme sua localização.

Obviamente, salve o arquivo *php.ini* com as edições realizadas.

Reinicie o serviço do *Apache* :  
```
service apache2 restart
```

Finalizada a instalação do servidor web *Apache* com suporte ao *PHP* .

## Instalando o GOLANG

Agora vamos fazer o download e instalar o pacote *GOLANG*.  
Primeiro vamos criar um novo diretório em downloads:  
```
mkdir /downloads/go -p
```

Acesse esse novo diretório:  
```
cd /downloads/go
```

Baixe e descompacte o pacote:  
```
wget https://golang.org/dl/go1.16.4.linux-amd64.tar.gz
tar -C /usr/local -zxvf go1.16.4.linux-amd64.tar.gz
```

O *GOLANG* foi instalado na pasta */usr/local* .  
Para funcionar corretamente, o *GO* espera que o sistema tenha um conjunto de variáveis de ambiente. Vamos criar um arquivo para automatizar a configuração das variáveis de ambiente necessárias:  
```
sudo vi /etc/profile.d/go.sh
```

Abaixo o conteúdo do arquivo:
```
#/bin/bash
export GOROOT=/usr/local/go
export GOPATH=$GOROOT/work
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

Salve e reinicie seu servidor:  
```
sudo reboot
```

Após o servidor reiniciado, verifique se as variáveis de ambiente necessárias foram criadas automaticamente:  
```
env | grep -E "(ROOT|GOPATH)"
```

O retorno correto, se seguido conforme esse tutorial, deve ser esse:
>GOROOT=/usr/local/go  
>GOPATH=/usr/local/go/work

Agora crie uma conta de usuário *Zabbix*. Dê com comando *sudo* , se necessário.  
Criando um novo grupo:  
```
groupadd zabbix
```

Adicionando o usuário:  
```
useradd -g zabbix -s /bin/bash zabbix
```

Instale os pacotes necessários:  
```
sudo apt-get update
sudo apt-get install build-essential libmysqlclient-dev libssl-dev libsnmp-dev libevent-dev pkg-config
sudo apt-get install libopenipmi-dev libcurl4-openssl-dev libxml2-dev libssh2-1-dev libpcre3-dev
sudo apt-get install libldap2-dev libiksemel-dev libcurl4-openssl-dev libgnutls28-dev
```

## Compilando e instalando o servidor Zabbix

Acesse o diretório onde baixamos:  
```
cd /downloads/zabbix-5.4.0
```

Compilando e instalando:  
```
sudo ./configure --enable-server --enable-agent --enable-agent2 --with-mysql --with-openssl --with-net-snmp --with-openipmi --with-libcurl --with-libxml2 --with-ssh2 --with-ldap --enable-ipv6
sudo make
sudo make install
```

Após o processo acima, encontre a localização do arquivo *zabbix_server.conf* .  
Primeiro, dê o comando abaixo:  
```
sudo updatedb
```

Logo após, encontre a localização do arquivo *zabbix_server.conf* no seu sistema:  
```
locate zabbix_server.conf
```

Após o comando acima, será apresentado o local onde se encontra o *zabbix_server.conf*.  
Edite o arquivo *zabbix_server.conf* :  
```
sudo vi /usr/local/etc/zabbix_server.conf
```

O arquivo original, antes da nossa configuração, estará assim:  
>LogFile=/tmp/zabbix_server.log  
>DBName=zabbix  
>DBUser=zabbix  
>Timeout=4  
>LogSlowQueries=3000  
>StatsAllowedIP=127.0.0.1  

Edite as linhas conforme abaixo:  
>LogFile=/tmp/zabbix_server.log  
>DBHost=localhost  
>DBName=zabbix  
>DBUser=zabbix  
>DBPassword=zabbix123  
>Timeout=4  
>LogSlowQueries=3000  
>StatsAllowedIP=127.0.0.1  

**NOTA:** Descomente a linha *DBPassword*

Salve o arquivo.

Logo após inicie o servidor *Zabbix* :  
```
/usr/local/sbin/zabbix_server
```

Use o seguinte comando para iniciar o agente *Zabbix* padrão:  
```
/usr/local/sbin/zabbix_agentd
```

Caso queira usar o novo agente (recomendo pesquisas sobre), dê o comando abaixo:  
```
/usr/local/sbin/zabbix_agent2 &
```

Mova todos os arquivos frontend do *Zabbix* para o diretório raiz de sua instalação *Apache* :  
```
mv /downloads/zabbix-5.4.0/ui /var/www/html/zabbix
```

Defina as permissões de arquivo:  
```
chown www-data.www-data /var/www/html/zabbix/* -R
```

Reinicie o serviço *Apache* :  
```
service apache2 restart
```

Feito isso, agora já será possível acessar a interface web do *Zabbix* e finalizar a instalação.

## Instalação da interface web Zabbix

Em qualquer máquina da rede, abra seu navegador web preferencial e digite o IP do seu servidor + */zabbix* . No exemplo utilizado aqui, será essa URL:
> http://192.168.0.100/zabbix  

Se tudo correu bem até aqui a interface de instalação web será apresentada:  
![IMG 01](https://res.cloudinary.com/k4bv734/image/upload/v1649289959/blog_content/zabbix_1_eiypec.png)

Selecione a linguagem desejada.  

**NOTA:** aqui só estarão disponíveis os idiomas conforme instalados no seu servidor. Caso deseje alguma linguagem diferente das disponíveis, instale no seu servidor, reinicie o serviço *Apache* e atualize a página da interface web. A configuração do idioma também pode ser feita posteriormente nas configuração do *Zabbix* via interface web.  
Clique no botão para avançar.

Na tela seguinte será apresentado o resultado dos requisitos necessários. Se seguiu conforme o tutorial, estará tudo OK.  
Clique em avançar:
![IMG 02](https://res.cloudinary.com/k4bv734/image/upload/v1649289959/blog_content/zabbix_2_xq7e2f.png)

Agora digite as informações do banco de dados conforme criado e clique para avançar:
>Database type: MySQL  
>Database host: localhost  
>Database port: 0  
>Database name: zabbix  
>Store credentials in: Plain text  
>User: zabbix  
>Password: zabbix123  

![IMG 03](https://res.cloudinary.com/k4bv734/image/upload/v1649289960/blog_content/zabbix_3_ak1moe.png)

Na próxima tela, não será necessária alteração.  
Clique para avançar:
![IMG 04](https://res.cloudinary.com/k4bv734/image/upload/v1649289959/blog_content/zabbix_4_dts2dl.png)

Agora selecione o fuso horário e tema desejado e avance:
![IMG 05](https://res.cloudinary.com/k4bv734/image/upload/v1649289959/blog_content/zabbix_5_go5nmi.png)

Veja o resumo da configuração e clique para avançar:
![IMG 06](https://res.cloudinary.com/k4bv734/image/upload/v1649289960/blog_content/zabbix_6_aorc3x.png)

Concluída a instalação é só clicar para finalizar:
![IMG 07](https://res.cloudinary.com/k4bv734/image/upload/v1649289960/blog_content/zabbix_7_jxspng.png)

Enfim será apresentada a tela para realizar login. Utilize as credenciais padrão:
>Usuário: Admin  
>Senha: zabbix  


**NOTA:** *Admin* com *A* maiúsculo.

![IMG 08](https://res.cloudinary.com/k4bv734/image/upload/v1649289960/blog_content/zabbix_8_nvxax1.png)

Feito o login você será redirecionado para o painel *Zabbix* .  
A instalação do *Zabbix* foi concluída com sucesso!
![IMG 09](https://res.cloudinary.com/k4bv734/image/upload/v1649289960/blog_content/zabbix_9_d1qlnb.png)