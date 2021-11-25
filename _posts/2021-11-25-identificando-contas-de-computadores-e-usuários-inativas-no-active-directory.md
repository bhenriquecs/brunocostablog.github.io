---
date: 2020-12-17 00:00:00
layout: post
title: Identificando contas de computadores e usuários inativas no Active Directory
description: Como identificar contas de computadores e usuários inativas no
  Active Directory.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/active-directory_ugsuli.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/active-directory_optimized_ckazmr.jpg
category: servidores
tags:
  - active directory
  - ""
author: brunocosta
paginate: false
---
É comum existir contas de computadores e de usuários no Active Directory que não estão mais em uso ou não existem mais na estrutura. Computadores formatados ou substituídos, usuários que não fazem mais parte do quadro da empresa e que continuam na listagem, pois não são removidos automaticamente do AD e não tivemos o devido cuidado com as boas práticas recomendadas. 

Abaixo uma opção de como localizar e remover essas contas antigas do nosso servidor:

Abra o CMD em modo administrador no servidor de domínio e execute o comando:  
Para computadores:  
`dsquery computer -inactive 10 -limit 0 >> c:\exportcomputer.csv` 


Para usuários execute:  
`dsquery user -inactive 10 -limit 0 >> c:\exportuser.txt`  


* O **10** significa a quantidade de semanas que o computador está inativo; 
* O **–limit 0** é para permitir a exibição de mais de 100 computadores no retorno; 
* O **c:\exportuser.txt** é o nome e diretório onde o arquivo será salvo.  

Poderá alterar as opções acima conforme seus critérios. 



Agora basta abrir as listas com um editor de texto de sua preferência, acessar o Active Directory e excluir os computadores e usuários listados.
