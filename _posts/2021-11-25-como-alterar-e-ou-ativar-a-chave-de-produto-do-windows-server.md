---
date: 2020-12-17 00:00:00
layout: post
title: Como alterar e/ou ativar a chave de produto do Windows Server
description: Como proceder para alterar ou ativar a chave de produto do Windows Server.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/chave-windows_spspp4.png
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/chave-windows_optimized_l8l0zw.jpg
category: windows
tags:
  - servidores
  - windows server
  - licença
  - ativação
author: brunocosta
paginate: false
---
Pode ocorrer, durante a instalação do Windows Server que a chave de produto não seja inserida ou reconhecida de forma correta. Nessas situações, o sistema é ativado em modo de avaliação por um período limitado com uma chave pré-definida. Com o término deste prazo, o sistema pode ficar indisponível.


Este tutorial tem como objetivo mostrar como inserir a chave de forma correta.


## Pré-requisitos:
* Servidor com Windows Server instalado;
* Chave de licenciamento da versão correta do sistema instalado.


## Passo 01 - Eliminar a chave pré-definida

* Abra o CMD com permissão elevada (como administrador);
* Digite o comando:  
`cscript.exe c:\windows\system32\slmgr.vbs -upk`



## Passo 02 - Adicionar nova chave 

* Ainda no CMD, insira o comando substituíndo os *AAAAA-AAAAA-AAAAA-AAAAA-AAAAA* por sua chave:  
`cscript.exe c:\windows\system32\slmgr.vbs -ipk AAAAA-AAAAA-AAAAA-AAAAA-AAAAA`

* Esse próximo comando, muitas das vezes não é necessário, pois o Windows já reconhece a chave na execução do comando anterior. Porém, para os casos que se fizer necessário, para ativar o sistema Windows basta executar o comando:  
`cscript.exe c:\windows\system32\slmgr.vbs -ato`

Pronto! Seu sistema estará corretamente ativado/licenciado.

Estes comandos também servem para aqueles que desejam e/ou necessitam alterar a chave de produto do Windows por qualquer outro motivo.