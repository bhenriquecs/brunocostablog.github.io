---
date: 2020-12-17 00:00:00
layout: post
title: Sincronizar horário entre Servidor Windows e Estação de trabalho
description: Como sincronizar horário entre um Servidor Windows e Estação de trabalho.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783287/blog/horario-servidor-sincronizar_xcsc9i.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/horario-servidor-sincronizar_optimized_dvp0wm.jpg
category: servidores
tags:
  - ntp
  - horário
  - sincronizar
author: brunocosta
paginate: false
---
Com um domínio em um servidor Windows bem configurado, normalmente não temos problemas em sincronização de horário entre o servidor e estação. Porém, se por algum motivo é necessário sincronizar o horário entre a estação e o servidor, indico abaixo alguns comandos para solucionar o problema.


Faça no computador/estação sem sincronização;


Abra o CMD como administrador;


* Comando para alterar o servidor NTP (em *server* você altera para o IP do seu servidor):  
`net time \\server /set /yes`




* Comandos para forçar uma atualização/sincronização:  
`w32tm /resync /rediscover`  
ou  
`w32tm /resync`

## Adicional

* Os comandos abaixo é para apontar um NTP externo. No exemplo, indico os servidores do <https://ntp.br/>:
```
net stop w32time
w32tm /config /manualpeerlist:a.ntp.br,b.ntp.br,c.ntp.br,0x8, /syncfromflags:manual 
net start w32time
```