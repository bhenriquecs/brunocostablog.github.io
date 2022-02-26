---
date: 2022-02-25 18:14:00
layout: post
title: Erro na despromoção de Controlador de Domínio (Domain Controller)
description: 'Uma solução para o erro "DFS Replication: Access is denied." ao
  tentar despromover um DC.'
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/active-directory_ugsuli.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/active-directory_optimized_ckazmr.jpg
category: servidores
tags:
  - ad
  - activedirectory
  - ""
author: brunocosta
paginate: false
---
Ao tentar despromover um Domain Controller problemático, podemos receber o seguinte retorno:

>The operation failed because:  
>DFS Replication: Access is denied.  
>"Access is denied."

No meu caso, o DC em questão estava sendo despromovido por inúmeros erros de replicação, onde havia em meu ambiente outros 4 DC's. Sendo assim, decidi despromover o servidor problemático para depois promove-lo novamente.  


Por inúmeros erros ocasionados pelo problema da replicação, não havia mais comunicação com o DC mestre de operações fazendo com que o erro citado fosse exibido. Realizei várias tentativas de tentar reparar a replicação, seja via ***dcdiag***, seja via outros caminhos que não citarei neste post, pois é um assunto mais extenso e cabe um melhor detalhamento em uma publicação mais informativa.  


Então, após algumas pesquisas e estudos, decidi fazer o seguinte: parar o serviço ***KDC*** e realizar uma nova tentativa de despromoção.
**Pronto! Resolvido o problema!** (pelo menos o da despromoção).  

Segue abaixo o que fazer e veja o quão simples foi:



No servidor que será despromovido, abra o ***CMD*** com privilégios administrativos.


Dê o comando:  
```net stop kdc```

Volte ao assistente para despromoção e prossiga com as ações normais da ação.


Quando exibida, marque a caixa para "forçar" a despromoção.


Siga conforme as etapas.



Para o caso do DC a ser despromovido seja ***Windows Server 2008*** ou anterior, utilize o ***DCPROMO***:


No servidor que será despromovido, abra o ***CMD*** com privilégios administrativos.


Dê o comando:  
```dcpromo```


Marque a caixa para "forçar" a despromoçãoe siga conforme as etapas.



Após a despromoção, como a mesma foi de maneira forçada, há a necessidade de limpar os metadados existentes nos demais DC's da rede (caso existam outros).
Veja como fazer em [Limpar metadados do Active Directory](https://brunocosta.dev/limpar-metadados-do-active-directory/).