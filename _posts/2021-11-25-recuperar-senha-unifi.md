---
date: 2020-12-18 00:00:00
layout: post
title: Recuperar senha do Unifi Controller
description: Recuperação da senha do Unifi Controller.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783289/blog/unifi_urlrde.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783289/blog/unifi_optimized_wcmlrw.jpg
category: tutorial
tags:
  - unifi
  - ubiquiti
  - recuperação
author: brunocosta
paginate: false
---
Para aqueles que possuem soluções da Ubiquiti (ecossistema Unifi) e por algum descuido (ou falha em seguir regras da documentação, haha), e perderam a senha de acesso ao Unifi Controller, existe uma opção de como recupera-la.

Veja a seguir:


Faça o download do MongoDB (<https://www.mongodb.com/try/download/community>).  
Escolha a opção .zip se usa Windows ou .tgz se utiliza Linux; 


No servidor onde se encontra instalado o ***Unifi Controller***, extraia o ***MongoDB*** baixado;


No Windows, abra o ***CMD*** como administrador e no Linux, o ***Terminal***;


Digite o comando para acessar a pasta bin existente no diretório do MongoDB.
**Não dê Enter ainda! **
Será algo do tipo (no Windows):  
`CD C:\Desktop\mongodb-windows-x86_64-4.4.2\bin`


Ainda nessa linha, após o ***"\bin"***, digite:  
`/mongo --port 27117`


Agora sim dê **Enter** para executar; 


Agora dê este comando:  
`use ace`


E por último este:  
`db.admin.find()`


No resultado serão exibidos o ***"name"*** e ***"x_password"***, que, como os nomes sugerem, são o usuário e senha, respectivamente;

Com os dados em mãos, basta acessar normalmente o painel do Unifi Controller. Sugiro realizar a troca da senha após o procedimento.

