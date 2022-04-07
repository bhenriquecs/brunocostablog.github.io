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

Agora, instale o serviço de banco de dados MySQL:
sudo apt-get install mysql-server mysql-client

Após a instalação, acesse a linha de comando de serviço MySQL:
mysql -u root -p

Crie um banco de dados chamado zabbix:
CREATE DATABASE zabbix CHARACTER SET UTF8 COLLATE UTF8_BIN;

Crie um usuário de banco de dados chamado zabbix. Note que estou definindo uma senha a esse usuário como "zabbix123":
CREATE USER 'zabbix'@'%' IDENTIFIED BY 'zabbix123';

Dê a esse usuário chamado zabbix permissões sobre o banco de dados chamado zabbix:
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'%';

Dê o comando abaixo para sair do CLI MySQL:
quit;

A partir de agora, vamos fazer o download o pacote de instalação Zabbix.
Para melhor organização, primeiro crie um novo diretório:
mkdir /downloads

Após a criação, acesse esse diretório pré-criado:
cd /downloads

Agora sim iremos fazer o download do Zabbix. Aqui iremos baixar a última versão estável disponível na data de publicação deste post (5.4):
sudo wget https://cdn.zabbix.com/zabbix/sources/stable/5.4/zabbix-5.4.0.tar.gz

Descompactando o pacote baixado:
tar -zxvf zabbix-5.4.0.tar.gz

Acessando diretório após descompactação:
cd zabbix-5.4.0/database/mysql/

Importação do modelo de banco de dados. Um comando por vez!:
mysql -u zabbix -p zabbix < schema.sql
mysql -u zabbix -p zabbix < images.sql
mysql -u zabbix -p zabbix < data.sql

Pronto! Finalizada a instalação do banco de dados Zabbix.
