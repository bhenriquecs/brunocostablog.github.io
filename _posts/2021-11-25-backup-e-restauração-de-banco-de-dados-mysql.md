---
date: 2020-12-17 00:00:00
layout: post
title: Backup e restauração de banco de dados MySQL
description: Maneira simples de fazer backup e restauração de banco de dados MySQL.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/mysql-bancodedados_uwcxuu.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/mysql-bancodedados_optimized_hlzyqw.jpg
category: bancodedados
tags:
  - mysql
  - backup
author: brunocosta
paginate: false
---
Maneira simples de fazer backup e restauração de banco de dados MySQL.



## Backup 
Abra o ***Prompt de Comando*** como administrador;


Acesse o diretório onde se encontra o MySQL:  
`CD C:\Program Files\MySQL\MySQL Server 5.5\bin`


Execute o comando:  
`mysqldump -u root -p bancodedados > C:\path\bk_bancodedados.sql`    


## Restauração
Abra o ***Prompt de Comando*** como administrador; 


Acesse o diretório onde se encontra o MySQL:  
`CD C:\Program Files\MySQL\MySQL Server 5.5\bin`


Execute o comando:  
`mysql.exe -u root –p bancodedados <C:\path\bk_bancodedados.sql`  

Onde:  
***bancodedados*** é o nome do banco;  
***path*** é o caminho onde se encontra ou irá salvar o backup do banco.
