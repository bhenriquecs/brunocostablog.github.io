---
date: 2020-12-17 00:00:00
layout: post
title: Criar e dar permissões de usuário no MySQL
description: Criar e dar permissões de usuário no MySQL.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783287/blog/mysql_c2jw8e.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/mysql_optimized_fymgqc.jpg
category: bancodedados
tags:
  - mysql
  - banco de dados
author: brunocosta
paginate: false
---
## Criando um novo usuário no SGBD MySQL


No Windows abra o CMD e dê o comando:  
`mysql`  


ou faça pela ferramenta ***MySQL Command-Line***

No Linux, no Terminal utilize o comando:  
`mysql -p`  
O ***p*** neste caso serve para a senha ser solicitada. Como o usuário não está sendo informado, será utilizado o nome de usuário logado no sistema. Para informar outro usuário utilize o comando ***-u***:  
` mysql -u root -p`  



Após o acesso, podemos utilizar a linha de comando para adicionar um novo usuário:
`CREATE USER 'novousuario'@'origem' IDENTIFIED BY 'senha';`  
Onde:  

***novousuario*** = nome que deseja para o novo usuário  
***origem*** = onde informamos a origem de onde o usuário terá permissão para conectar ao banco. Pode ser:  
* ***localhost*** = somente acesso local  
* ***%*** = acesso de qualquer origem  
* ***IP*** = acesso de um IP específico  

***senha*** = obviamente, senha para o usuário



Exemplos:
* `CREATE USER 'novousuario'@'localhost' IDENTIFIED BY 'password';`
* `CREATE USER 'novousuario'@'%' IDENTIFIED BY 'password';`
* `CREATE USER 'novousuario'@'192.168.1.1' IDENTIFIED BY 'password';`   


Para excluir um usuário, utilizamos o comando ***DROP USER*** utilizando a mesma maneira de acesso na criação de usuário:  
`DROP USER 'usuario'@'localhost';`



O usuário criado ainda não tem nenhuma permissão de acesso a nenhum banco de dados, então vamos conceder alguma permissão. Veja os exemplos:


`GRANT ALL PRIVILEGES ON * . * TO 'usuarioexemplo'@'localhost';`  
Concede permissões totais ao usuário "usuarioexemplo"

`GRANT ALL PRIVILEGES ON banco01.* TO 'usuarioexemplo'@'localhost';`  
Concede permissões totais ao "usuarioexemplo" ao banco de dados "banco01" em todas as tabelas com acesso local    

`GRANT SELECT ON banco02.usuarios TO 'usuarioexemplo'@'%';`  
Concede permissão de leitura na tabela "usuarios" no banco de dados "banco02" para o usuário "usuarioexemplo" com acesso de qualquer local 


Depois de finalizadas as permissões desejadas, é importante recarregar os privilégios com o comando:  
`FLUSH PRIVILEGES;`


Tipos de permissões que poderão ser concedidas aos usuários:
* **ALL PRIVILEGES** – Como mostrado no exemplo anterior, esta opção dá acesso total a um banco de dados ou a todo o sistema se nenhum banco de dados for selecionado;  
* **CREATE** – permite criar novas tabelas ou bases de dados;  
* **DROP** – permite deletar tabelas ou bases de dados;  
* **DELETE** – permite deletar linhas das tabelas;  
* **INSERT** – permite inserir linhas nas tabelas;  
* **SELECT** – permite utilizar o comando SELECT para ler bases de dados;  
* **UPDATE** – permite atualizar linhas das tabelas;  
* **GRANT OPTION** – permite conceder ou revogar privilégios de outros usuários.  
