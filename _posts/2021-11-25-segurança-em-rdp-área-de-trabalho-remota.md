---
date: 2020-12-17 00:00:00
layout: post
title: Segurança em RDP - Área de Trabalho Remota
description: Algumas dicas de segurança em servidores de Área de Trabalho Remota.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/rdp_pp3eam.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/rdp_optimized_jo5hw8.jpg
category: ciberseguranca
tags:
  - RDP
  - cibersegurança
  - remoto
author: brunocosta
paginate: false
---
Algumas dicas de segurança em servidores de Área de Trabalho Remota.
## Como investigar e evitar ataques ao seu servidor online?



* Utilize sistemas atualizados, e, se possível, na última versão disponível (No Windows, Windows Server 2019, por exemplo);


* Tenha uma solução de segurança firewall e endpoint robusta instalada e devidamente configurada, seguindo os protocolos sugeridos pelo desenvolvedor. Exemplo de desenvolvedores e fornecedores de soluções de segurança: Sophos, Fortinet, Trend Micro, Symantec, ESET;


* Acompanhar e verificar os Eventos de Logon no Visualizador de Eventos (eventvwr.msc), principalmente os IDs;


* Verificar se nenhuma conta local foi criada sem consentimento no servidor. Desative e/ou exclua as contas locais existentes que não serão utilizadas;


* Troque a porta de acesso. O padrão é a 3389;


* Exija senhas complexas para todas as contas de usuários;


* Se for possível, configure que somente IPs específicos tenham acesso ao servidor.
