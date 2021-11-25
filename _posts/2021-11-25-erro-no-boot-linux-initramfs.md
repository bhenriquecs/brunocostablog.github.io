---
date: 2020-12-29 00:00:00
layout: post
title: Erro no boot Linux (initramfs)
description: Erro "initramfs" na tentativa de inicialização do sistema.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783287/blog/initramfs_wuwsz0.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783287/blog/initramfs_optimized_ye7cry.jpg
category: linux
tags:
  - linux
  - boot
  - initramfs
author: brunocosta
paginate: false
---
Um erro que pode ocorrer e assustar os iniciantes no mundo open source Linux é o ***"initramfs"*** na tentativa de inicialização do sistema.


Esse ocorre por problemas no sistema de arquivos e pode ser causado por:
* Desligamento por força bruta, cortando a energia elétrica inesperadamente
* Particionamento com defeito
* HD com defeito. Neste caso sugiro a substituição caso o problema se torne constante


## Passos para corrigir o problema 

Anote/salve a partição ou disco indicado no erro;


Você deve ter um disco ou pendrive com uma distribuição Linux para rodar em ***"live"***;


Insira/conecte e dê boot por esse dispositivo;


Após completar a inicialização em ***"live"***, abra o ***Terminal***;


Dê o comando abaixo para identificarmos a partição ou disco com problemas:  
`sudo fdisk -l` 


Verifique a partição/disco que foi mencionado no erro;


Agora para corrigir execute o seguinte comando (substitua ***/dev/sda0*** pela sua partição com problemas):  
`sudo fsck -y /dev/sda0`


Se solicitar senha, digite sua senha com acesso root; 


Pronto! Finalizada a correção, poderá reiniciar com o comando:   
`sudo reboot` 


Retire a mídia ***"live"*** e inicie seu sistema normalmente.
