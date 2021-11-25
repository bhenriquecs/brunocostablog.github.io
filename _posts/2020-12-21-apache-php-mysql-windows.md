---
date: 2020-12-21T12:00:00.000Z
layout: post
title: Apache + PHP + MySQL no Windows
subtitle: Como montar um servidor web com Apache com suporte ao PHP e MySQL sem
  usar pacotes prontos como o WAMP e XAMP?
description: Como montar um servidor web com Apache com suporte ao PHP e MySQL
  sem usar pacotes prontos como o WAMP e XAMP?
image: https://res.cloudinary.com/k4bv734/image/upload/v1637696792/blog/apache_aqldc8.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637696792/blog/apache_optimized_a0make.jpg
category: servidores
tags:
  - webserver
  - servidorweb
  - apache
  - mysql
  - PHP
author: brunocosta
paginate: true
---
Aqui iremos tratar somente as instalações e configurações iniciais para funcionamento padrão, não entraremos nas demais configurações que cada ferramenta possui.  
Antes de tudo, recomendo a leitura das documentações oficiais de cada ferramenta/solução:

>Apache: <http://httpd.apache.org/docs/current/platform/windows.html>  
>PHP: <https://www.php.net/manual/en/index.php>  
>MySQL: <https://dev.mysql.com/doc>

## Apache

O Apache não fornece binários para Windows, porém existem várias opções de terceiros disponíveis para download, como por exemplo o Apache Lounge e Apache Haus.  
Baixe a versão correta para o seu sistema operacional, x86 (32 bits) ou x64 (64 bits):

>32 bits: <https://www.apachelounge.com/download/VS16/binaries/httpd-2.4.46-win32-VS16.zip>  
>64 bits: <https://www.apachelounge.com/download/VS16/binaries/httpd-2.4.46-win64-VS16.zip>

Baixe e instale também o Visual C ++ Redistributable para Visual Studio 2015-2019, caso seu sistema não o tenha. Também escolha a versão apropriada.

>32 bits: <https://aka.ms/vs/16/release/VC_redist.x86.exe>  
>64 bits: <https://aka.ms/vs/16/release/VC_redist.x64.exe>

Descompacte o apache baixado na raiz do seu disco (geralmente C:\). Você terá algo como ***C:\Apache24*** .  
Abra o CMD (Prompt de comando) e vá até o diretório ***C:\Apache24\bin*** .
Execute:  
```
httpd.exe
```

O firewall do Windows pode pedir permissão para o Apache se comunique em específicas redes. Sugiro aceitar em redes domésticas e corporativas e não permitir em redes públicas.  
O Apache já está instalado. Para conferir abra um navegador e acesse ***http://localhost***. Se aparecer a página com os dizeres ***"It Works!"*** significa que o Apache está funcionando corretamente.  
Caso receba algum aviso sobre "não poder determinar o nome do domínio totalmente qualificado", faça o seguinte:
* Com um editor de texto, abra o arquivo httpd.conf, existente no diretório ***C:\Apache24\conf***
* Encontre `ServerName <yourhostname>`. Descomente e altere `<yourhostname>` por `<localhost>` ou pelo `<nome do host>` do sistema
* Salve o arquivo

Para executar o Apache automaticamente sempre que o sistema for iniciado, sem a necessidade de fazer login ou executar o serviço manualmente, vamos transformá-lo em um serviço do Windows.
* Abra o CMD como administrador (caso tenha o fechado)
* Vá até o diretório ***C:\Apache24\bin***
* Dê o comando:  
```
httpd.exe -k install
```

Pronto! Agora você tem o Apache instalado como serviço do Windows o qual poderá gerenciar no Serviços (services.msc).

## PHP

Baixe o PHP versão TS (Thread Safe) correspondente ao seu sistema (x86 ou x64), na [página oficial](https://windows.php.net/download/) de download do PHP para Windows. Sugiro a versão mais recente disponível, porém fica a critério dos seus requisitos.  

Crie uma pasta nomeada como "php" na raiz do seu disco ***C:\php***.  
Extraia o arquivo baixado anteriormente nesta pasta.  

Acesse o diretório ***C:\php*** e renomeie o ***php.ini-production*** ou ***php.ini-development*** (somente um desses) para ***php.ini***, levando em consideração se está instalando para produção ou em ambiente de desenvolvimento/testes.  

Abra esse ***php.ini*** com um editor de textos (recomendo o Notepad++) e pesquise por ***extension_dir = "ext"***. Será necessário desmarcar essa linha como comentário, para isso remova o ***;*** (ponto e vírgula) que inicia a sentença. Isso é pra definir o diretório padrão de extensões para ***C:\php\ext***.  

Agora vamos configurar o Apache para usar esse PHP. Primeiro vamos parar o serviço do Apache. Abra o ***Serviços do Windows*** (win + R e digite ***services.msc***), encontre o serviço do Apache e clique em Parar.  

Abra o arquivo ***httpd.conf***, existente no diretório ***C:\Apache24\conf*** com um editor de texto e adicione o seguinte:  

Para o PHP 7
```
LoadModule php7_module "c:\php\php7apache2_4.dll"
  <IfModule php7_module>
    AddHandler application/x-httpd-php .php
    AddType application/x-httpd-php .php .html
    PHPIniDir "c:\php"
  </IfModule>
```

Para o PHP 5
```
LoadModule php5_module C:/PHP/php5apache2_4.dll
  <IfModule php5_module>
    DirectoryIndex index.html index.php
    AddHandler application/x-httpd-php .php
    PHPIniDir "C:/PHP"
  </IfModule>
```

Agora execute o Apache manualmente utilizando o CMD.
* Abra o CMD como administrador  
* Vá até o diretório ***C:\Apache24\bin***  
* Execute: 
```
httpd.exe
```

Se não houver erros quer dizer que ocorreu tudo bem com sua configuração e você poderá testar o PHP.  
Crie um arquivo nomeado como phpinfo.php
* Digite `<?php phpinfo();?>` no arquivo
* Salve no diretório ***C:\Apache24\htdocs***
* Abra o navegador e acesse <http://localhost/phpinfo.php>
* Se tudo tiver certo, você verá uma página com algumas informações do seu sistema. Caso retorne alguma algo como ***"Erro interno do servidor"***, significa que algo está errado. Verifique as configurações feitas até aqui.

Se seguiu exatamente como neste tutorial, o CMD ainda estará aberto com o serviço do Apache iniciado. "Mate" o serviço com Crtl + C

Agora você pode iniciar o serviço do Apache no Serviços do Windows e pronto!

## MySQL (ou MariaDB)

Primeiramente já recomendo habilitar as extensões que permitirão o acesso ao banco de dados utilizando o PHP:  
* Acesse o diretório ***C:\php*** e abra com um editor de texto o ***php.ini***  
* Habilite as extensões tirando o ***;*** (ponto e vírgula) do início das sentenças ***php_mysqli*** e ***php_pdo_mysql***

Baixe o MySQL ou MariaDB na página oficial de download.  
> MySQL: <https://dev.mysql.com/downloads/installer>  
> MariaDB: <https://mariadb.org/download>  

Execute o instalador .msi baixado, seguindo as instruções e melhores práticas de instalação. Não irei entrar em outras considerações de configurações do MySQL neste momento, pois é uma assunto extenso e caberá em um post a parte.  

Pronto, agora você tem um servidor web Apache com PHP e MySQL configurado. Bora pro desenvolvimento!