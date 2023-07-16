---
date: 2023-01-03 19:00:24
layout: post
title: Identificando um firewall de aplicativo da Web (WAF)
description: Identificando um firewall de aplicativo da Web (WAF)
image: https://res.cloudinary.com/k4bv734/image/upload/v1689536360/waf_q61cuu.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689536360/waf_optimized_ooub1l.jpg
category: ciberseguranca
tags:
  - waf
  - cybersecurity
author: brunocosta
paginate: false
---
> **Aviso: Conteúdo Sensível em Cibersegurança**

> Este aviso tem o objetivo de informar sobre a natureza sensível do conteúdo relacionado à cibersegurança que será abordado neste texto. O conteúdo a seguir foi criado com fins puramente educacionais e para pesquisa, visando a conscientização e a compreensão dos desafios enfrentados na proteção de sistemas e informações digitais.

Este artigo explicará algumas das ferramentas e técnicas usadas por testadores de penetração de aplicativos da web e pesquisadores de segurança para identificar com sucesso as proteções do firewall de aplicativos da web (WAF).

Os WAFs são uma solução de segurança cibernética para filtrar e bloquear tráfego da web malicioso. Os fornecedores comuns incluem CloudFlare, AWS, Citrix, Akamai, Microsoft Azure, entre outros.

## Identificando WAFs

### Manualmente

1. Os WAFs geralmente bloqueiam tráfego abertamente malicioso. Para acionar um firewall e verificar sua existência, pode-se fazer uma solicitação HTTP para o aplicativo da web com uma consulta maliciosa na URL, como `https://example.com/?p4yl04d3=<script>alert(document.cookie)</script>`. A resposta HTTP pode ser diferente do esperado para a página da web que está sendo visitada. O WAF pode retornar sua própria página da web ou um código de status diferente, geralmente na faixa de 400.

2. Através de um proxy da web, cURL ou da guia "Rede" das ferramentas de desenvolvimento do seu navegador, é possível detectar indicações adicionais de um firewall:
   - O nome do WAF no cabeçalho do servidor (por exemplo, `Server: cloudflare`)
   - Cabeçalhos de resposta HTTP adicionais associados ao WAF (por exemplo, `CF-RAY: xxxxxxxxxxx`)
   - Cookies que parecem ser definidos por um WAF (por exemplo, o cabeçalho de resposta `Set-Cookie: __cfduid=xxxxx`)
   - Código de resposta exclusivo ao enviar solicitações maliciosas (por exemplo, 412)

Além de criar consultas maliciosas e avaliar a resposta, os firewalls também podem ser detectados enviando um pacote TCP FIN/RST para o servidor ou implementando um ataque de canal lateral. Por exemplo, o tempo de resposta do firewall em relação a diferentes cargas úteis pode dar pistas sobre o WAF usado.

### Automação

A seguir estão três métodos automatizados de detecção e identificação de WAFs.

**1. Executando uma varredura Nmap**

A Engine de Scripts do Nmap (NSE) inclui scripts para detectar e identificar firewalls. Exemplo de uso:

~~~
$ nmap --script=http-waf-fingerprint,http-waf-detect -p443 example.com
Starting Nmap 7.93 (https://nmap.org) at 2023-05-29 21:43 PDT
Nmap scan report for example.com (xxx.xxx.xxx.xxx)
Host is up (0.20s latency).

PORT    STATE SERVICE
443/tcp open  https
| http-waf-detect: IDS/IPS/WAF detected:
|_example.com:443/?p4yl04d3=<script>alert(document.cookie)</script>

Nmap done: 1 IP address (1 host up) scanned in 8.81 seconds
~~~
**2. WhatWaf**

Além de detectar um firewall, o WhatWaf pode tentar descobrir uma forma de contorná-lo usando scripts de adulteração e avaliando a resposta do servidor da web às várias cargas úteis.

**3. WafW00f**

O Wafw00f é uma ferramenta de linha de comando que envia cargas úteis comumente identificadas para o nome de domínio fornecido e avalia a resposta do servidor da web para detectar e identificar o firewall, quando possível. Exemplo de uso:
~~~
$ wafw00f example.com
~~~


Os resultados do Wafw00f são consistentes como os do WhatWaf.




Vimos algumas das maneiras de identificar um WAF.
