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
```sudo apt-get update``` 
 
Atualiza o sistema, realiza o download e instala atualizações de pacotes e dos programas do servidor:  
```sudo apt-get upgrade```

## Instalando e preparando o banco de dados



Instale o serviço de banco de dados MySQL:  
```sudo apt-get install mysql-server mysql-client```  

Após a instalação, acesse a linha de comando de serviço MySQL:  
```mysql -u root -p```  


Crie um banco de dados chamado zabbix:  
```CREATE DATABASE zabbix CHARACTER SET UTF8 COLLATE UTF8_BIN;```  

Crie um usuário de banco de dados chamado zabbix. Note que estou definindo uma senha a esse usuário como "zabbix123":  
```CREATE USER 'zabbix'@'%' IDENTIFIED BY 'zabbix123';```

Dê a esse usuário chamado zabbix permissões sobre o banco de dados chamado zabbix:  
```GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'%';```

Dê o comando abaixo para sair do CLI MySQL:  
```quit;```

A partir de agora, vamos fazer o download o pacote de instalação Zabbix.
Para melhor organização, primeiro crie um novo diretório:  
```mkdir /downloads```

Após a criação, acesse esse diretório pré-criado:  
```cd /downloads```

Agora sim iremos fazer o download do Zabbix. Aqui iremos baixar a última versão estável disponível na data de publicação deste post (5.4):  
```sudo wget https://cdn.zabbix.com/zabbix/sources/stable/5.4/zabbix-5.4.0.tar.gz```

Descompactando o pacote baixado:  
```tar -zxvf zabbix-5.4.0.tar.gz```

Acessando diretório após descompactação:  
```cd zabbix-5.4.0/database/mysql/```

Importação do modelo de banco de dados. Um comando por vez!  
```mysql -u zabbix -p zabbix < schema.sql```  
```mysql -u zabbix -p zabbix < images.sql```  
```mysql -u zabbix -p zabbix < data.sql```  

Pronto! Finalizada a instalação do banco de dados Zabbix.

## Instalando o servidor web

Instale o servidor web Apache e todos os pacotes necessários:  
```sudo apt-get install apache2 php libapache2-mod-php php-cli php-mysql php-mbstring php-gd php-xml php-bcmath php-ldap mlocate```

Dê o comando abaixo:  
```sudo updatedb```

Logo após, encontre a localização do arquivo php.ini no seu sistema:  
```locate php.ini```

Após o comando acima, será apresentado o local onde se encontra o php.ini.
Edite o arquivo php.ini. Aqui iremos utilizar o Vi, porém fique a vontade pra utilizar o editor de textos de sua preferência:  
```sudo vi /etc/php/7.4/apache2/php.ini```

No php.ini, defina os seguintes itens conforme abaixo:  
```
max_execution_time = 300
memory_limit = 256M
post_max_size = 32M
max_input_time = 300
date.timezone = America/Sao_Paulo
```
NOTA: O date.timezone edite conforme sua localização.

Obviamente, salve o arquivo php.ini com as edições realizadas.

Reinicie o serviço do Apache:  
```service apache2 restart```

Finalizada a instalação do servidor web Apache com suporte ao PHP.

## Instalando o GOLANG

Agora vamos fazer o download e instalar o pacote GOLANG.  
Primeiro vamos criar um novo diretório em downloads:  
```mkdir /downloads/go -p```

Acesse esse novo diretório:  
```cd /downloads/go```

Baixe e descompacte o pacote:  
```wget https://golang.org/dl/go1.16.4.linux-amd64.tar.gz```  
```tar -C /usr/local -zxvf go1.16.4.linux-amd64.tar.gz```

O GOLANG foi instalado na pasta /usr/local.  
Para funcionar corretamente, o GO espera que o sistema tenha um conjunto de variáveis de ambiente. Vamos criar um arquivo para automatizar a configuração das variáveis de ambiente necessárias:  
```sudo vi /etc/profile.d/go.sh```

Abaixo o conteúdo do arquivo:
```
#/bin/bash
export GOROOT=/usr/local/go
export GOPATH=$GOROOT/work
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

Salve e reinicie seu servidor:  
```sudo reboot```

Após o servidor reiniciado, verifique se as variáveis de ambiente necessárias foram criadas automaticamente:  
```env | grep -E "(ROOT|GOPATH)"```

O retorno correto, se seguido conforme esse tutorial, deve ser esse:
>GOROOT=/usr/local/go  
>GOPATH=/usr/local/go/work


Agora crie uma conta Linux para o usuário Zabbix. Dê com comando sudo, se necessário.  
Criando um novo grupo:  
```groupadd zabbix```

Adicionando o usuário:  
```useradd -g zabbix -s /bin/bash zabbix```

Instale os pacotes necessários:  
```sudo apt-get update```  
```sudo apt-get install build-essential libmysqlclient-dev libssl-dev libsnmp-dev libevent-dev pkg-config```  
```sudo apt-get install libopenipmi-dev libcurl4-openssl-dev libxml2-dev libssh2-1-dev libpcre3-dev```  
```sudo apt-get install libldap2-dev libiksemel-dev libcurl4-openssl-dev libgnutls28-dev```

