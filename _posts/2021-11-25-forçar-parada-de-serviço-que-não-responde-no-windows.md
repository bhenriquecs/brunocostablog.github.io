---
date: 2020-12-17 00:00:00
layout: post
title: Forçar parada de serviço que não responde no Windows
description: Forçar parada de serviço que não responde no Windows.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783289/blog/servico-windows_tnl0gs.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783289/blog/servico-windows_optimized_rrcgym.jpg
category: windows
tags:
  - serviço
  - windows
author: brunocosta
paginate: false
---
Se algum serviço está "travado" e se recusa a responder ao comando na tentativa de parar o processo mesmo no ***Gerenciador de Tarefas***, siga as instruções a seguir:


Tecle **Win + R** ou **Menu Iniciar**;

Execute ou pesquise ***services.msc***;

Na janela que será aberta procure o serviço problemático na lista, clique com o direito e vá em ***Propriedades***;

Anote/copie o nome do serviço;
![IMG 01](https://res.cloudinary.com/k4bv734/image/upload/v1637862789/blog_content/servico-windows_1_nt2ana.png)

Abra o ***CMD*** (Prompt de Comando) e digite:  
`sc queryex nomedoserviço`  
Dê enter e identifique o ***PID***;
![IMG 02](https://res.cloudinary.com/k4bv734/image/upload/v1637862789/blog_content/servico-windows_2_pv3cal.png)

Na mesma janela do CMD digite;  
`taskkill /pid númerodopid] /f` 

Dê enter e o serviço será parado. Verifique no ***Serviços*** (services.msc).