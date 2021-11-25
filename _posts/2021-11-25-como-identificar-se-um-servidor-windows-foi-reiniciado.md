---
date: 2020-12-17 00:00:00
layout: post
title: Como identificar se um servidor Windows foi reiniciado?
description: Como identificar se um servidor Windows foi reiniciado?
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783289/blog/windows-reiniciando_jimbqc.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783289/blog/windows-reiniciando_optimized_k3g0xr.jpg
category: servidores
tags:
  - servidores
  - windows server
  - restart
author: brunocosta
paginate: false
---
Existem alguns eventos do ***Event Viewer*** (Visualizador de Eventos) do Windows que podem identificar quando os servidores existentes foram reiniciados.



Para isso, acesse o ***Visualizador de Eventos*** em ***Ferramentas Administrativas*** ou pelo comando ***"eventvwr"***;


Navegue até o tipo ***System*** (Sistema);


Filtre nos logs pelas IDs 1074, 1076, 6009, 6005 e 6013.