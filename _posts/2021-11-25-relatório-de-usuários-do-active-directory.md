---
date: 2020-12-17 00:00:00
layout: post
title: Relatório de usuários do Active Directory
description: Como extrair um relatório de usuários existentes no Active Directory.
category: servidores
tags:
  - activedirectory
  - ""
author: brunocosta
paginate: false
---
Aqui uma maneira de extrair um relatório de usuários existentes no seu Active Directory.

No **CMD** execute o comando:  
`dsquery user domainroot -limit 3000 |dsget user -display -samid -disabled > C:\path\users_ad.txt`  

Sendo ***C:\path*** o caminho do diretório onde irá salvar o arquivo com os dados extraídos, e ***users_ad.txt*** o nome e extensão do arquivo.

Mais informações procure sobre ***DSQUERY*** nas documentações da Microsoft.