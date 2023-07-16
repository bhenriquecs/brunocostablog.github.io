---
date: 2022-10-07 08:30:00
layout: post
title: Portas para Replicação entre Controladores de Domínio via VPN
description: Portas para Replicação entre Controladores de Domínio via VPN
image: https://res.cloudinary.com/k4bv734/image/upload/v1689532913/replicacao-active-directory2_ptex3b.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689532912/replicacao-active-directory2_optimized_ze1gt5.jpg
category: servidores
tags:
  - windowsserver
  - activerdirectory
  - ad
  - vpn
  - replicação
author: brunocosta
paginate: false
---
Para garantir a replicação adequada entre controladores de domínio em locais diferentes conectados via VPN, é necessário abrir as seguintes portas no firewall:

- **TCP/UDP 389**: Essa porta é usada para a replicação de diretórios do Active Directory e permite a comunicação através do protocolo LDAP (Lightweight Directory Access Protocol) entre os controladores de domínio.

- **TCP/UDP 636**: Se você estiver usando comunicações seguras (LDAPS - Lightweight Directory Access Protocol over SSL/TLS), é necessário abrir essa porta. Ela é utilizada para comunicação LDAP criptografada e segura.

- **TCP 3268**: Essa porta é utilizada para consultas globais do Active Directory e deve ser aberta se você tiver múltiplos domínios em seu ambiente e precisar consultar informações em todos eles.

- **TCP 3269**: Se você estiver utilizando consultas globais com comunicação segura (LDAPS do catálogo global), é necessário abrir essa porta. Ela é usada para comunicação segura e criptografada com o catálogo global.

- **TCP 88**: Essa porta é utilizada pelo Kerberos, um protocolo de autenticação usado pelo Active Directory. É necessário abrir essa porta para permitir a autenticação entre os controladores de domínio.

- **TCP/UDP 53**: Essa porta é usada pelo serviço DNS (Domain Name System) e deve estar aberta para permitir a resolução de nomes entre os controladores de domínio e garantir a replicação correta das informações DNS.

Essas são as portas principais que precisam ser abertas para permitir a comunicação e replicação entre controladores de domínio em locais diferentes via VPN. No entanto, dependendo da configuração específica do seu ambiente e dos serviços adicionais que você estiver utilizando, pode ser necessário abrir outras portas específicas. Certifique-se de revisar a documentação do seu fornecedor de firewall ou consultar o suporte técnico para obter informações detalhadas sobre as portas necessárias para o seu caso específico.
