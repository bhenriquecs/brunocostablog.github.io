---
date: 2022-02-25 20:42:49
layout: post
title: Limpar metadados do Active Directory
description: A limpeza de metadados é um procedimento necessário após uma remoção forçada.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/active-directory_ugsuli.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/active-directory_optimized_ckazmr.jpg
category: servidores
tags:
  - ad
  - activedirectory
  - metadados
author: brunocosta
paginate: false
---
A limpeza de metadados é um procedimento necessário após uma remoção forçada de Active Directory Domain Services (AD DS).  
Há duas vias para limpar os metadados do servidor:
* usando ferramentas do ambiente gráfico do sistema
* usando a linha de comando

## Limpado metadados do servidor usando Usuários e Computadores do Active Directory

Pesquise no Menu Iniciar ou vá diretamente através das ***Ferramentas Administrativas***, e abra o ***Usuários e Computadores do Active Directory***.
![Img 01](https://res.cloudinary.com/k4bv734/image/upload/v1645832545/blog_content/limpar-metadados_1_kkggpf.png)

Na lista da esquerda, expanda o domínio do controlador de domínio e clique em ***Controladores de Domínio***.

![Img 02](https://res.cloudinary.com/k4bv734/image/upload/v1645832546/blog_content/limpar-metadados_2_jvqgh4.png)

No painel de detalhes à direita, clique com o botão direito do mouse no objeto de computador do controlador de domínio cujos metadados você deseja limpar e clique em ***Excluir***.
![Img 03](https://res.cloudinary.com/k4bv734/image/upload/v1645832546/blog_content/limpar-metadados_3_l8h2oh.png)

Na caixa de diálogo que surgirá, confirme se o nome do controlador de domínio que você deseja excluir é mostrado e clique em ***Sim*** para confirmar a exclusão do objeto do computador.  

Na caixa de diálogo ***Excluindo Controlador de Domínio***, selecione ***Este Controlador de Domínio está permanentemente offline e não pode mais ser rebaixado usando o DCPROMO*** e clique em ***Excluir***.  

Se o controlador de domínio for um servidor de catálogo global, na caixa de diálogo ***Excluir Controlador de Domínio***, clique em ***Sim*** para continuar.  

Se o controlador de domínio tiver atualmente uma ou mais funções mestras de operações, clique em ***OK*** para mover a função ou funções para o controlador de domínio mostrado. Não é possível alterar esse controlador de domínio. Se você quiser mover a função para um controlador de domínio diferente, deverá mover a função depois de concluir o procedimento de limpeza de metadados do servidor.  

## Limpar metadados do servidor usando Serviços e Sites do Active Directory

Abra ***Serviços e Sites do Active Directory***.  
![Img 04](https://res.cloudinary.com/k4bv734/image/upload/v1645832546/blog_content/limpar-metadados_4_umcorg.png)


Na lista da esquerda expanda os níveis: ***Sites > domínio > Servers***.  


Após expanda o nome do controlador de domínio, clique com o botão direito do mouse no objeto ***NTDS Configurações*** e clique em ***Excluir***.  
![Img 05](https://res.cloudinary.com/k4bv734/image/upload/v1645832546/blog_content/limpar-metadados_5_lfg5iy.png)

Na caixa de diálogo, clique em ***Sim*** para confirmar a exclusão.  

Na caixa de diálogo ***Excluindo Controlador de Domínio***, selecione ***Este Controlador de Domínio está permanentemente offline e não pode mais ser rebaixado usando o DCPROMO*** e clique em ***Excluir***.  

Se o controlador de domínio for um servidor de catálogo global, na caixa de diálogo ***Excluir Controlador de Domínio***, clique em ***Sim*** para continuar com a exclusão.  

Se o controlador de domínio tiver atualmente uma ou mais funções mestras de operações, clique em ***OK*** para mover a função ou funções para o controlador de domínio mostrado.

Clique com o botão direito do mouse no controlador de domínio que foi removido à força e clique em ***Excluir***.  

Na caixa de diálogo, clique em ***Sim*** para confirmar a exclusão do controlador de domínio.  

## Limpar metadados do servidor usando linha de comando

Como alternativa, você pode limpar metadados usando o ntdsutil.exe, uma ferramenta de linha de comando instalada automaticamente em todos os controladores de domínio.

Abra um ***prompt de comando (CMD)*** como administrador.  

No prompt de comando, digite o seguinte comando e pressione ***Enter***:  
```Ntdsutil```

No ***ntdsutil:*** digite o seguinte comando e pressione ***Enter***:  
```metadata cleanup```

No ***metadata cleanup:***, digite o comando abaixo e pressione ***Enter*** novamente:  
```remove selected server <NomedoServidor>```

Na caixa de diálogo ***Remover Configuração do Servidor***, revise as informações e o aviso e clique em ***Sim*** para remover o objeto e os metadados do servidor. Neste ponto, o ***Ntdsutil*** confirma que o controlador de domínio foi removido com êxito.

Para sair da ferramenta, dê o comando ```quit``` e pressione ***Enter***.

Para confirmar a remoção do controlador de domínio, acesse o ***Usuários e Computadores do Active Directory*** e ***Serviços e Sites do Active Directory***, e veja que o servidor já não estará na árvore de DCs.

