---
date: 2020-12-17 00:00:00
layout: post
title: Alterando a velocidade de rolagem do mouse no Linux
description: Um "problema" que tive no Linux, na distro Ubuntu, era na
  velocidade do botão de rolagem do mouse. Por padrão tive muita lentidão nas
  rolagem de páginas.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783287/blog/linux-mouse_rh1ghm.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783287/blog/linux-mouse_optimized_hwgsmo.jpg
category: blog
tags:
  - linux
  - ubuntu
  - mouse
author: brunocosta
paginate: false
---
Um "problema" que tive no Linux, na distro Ubuntu (para aqueles que estão iniciando em Linux, este é baseado no Debian), era na velocidade do botão de rolagem do mouse. Por padrão tive muita lentidão nas rolagem de páginas.

Para resolver, utilizei o Inwheel. Aqui estarei utilizando como base o Ubuntu 20.04.

## Instalando o Imwheel
Abra o ***Terminal*** (Crtl + Alt + T);  
Dê o comando abaixo e digite sua senha root;  
`sudo apt-get install imwheel`

## Configuração
Baixe ou crie um novo documento ***Bash*** (.sh) com o script existente neste link
<http://www.nicknorton.net/mousewheel.sh> (Obrigado!);

Se você for iniciante no mundo Linux, pode encontrar alguma dificuldade na tarefa acima. Um exemplo de como poderá ser feito de forma simples e utilizando o ambiente gráfico:  
* Clique no link que contém o script;
* Copie o script;
* Abra o menu de aplicativos e execute o ***Editor de texto***;
![Img 01](https://res.cloudinary.com/k4bv734/image/upload/v1637846612/blog_content/linux-mouse-content_1_qqols8.png)

* No Editor de texto cole o script copiado anteriormente;
* Clique em ***Salvar***, escolha um diretório e salve com o nome ***mousewheel.sh***;
![Img 02](https://res.cloudinary.com/k4bv734/image/upload/v1637846612/blog_content/linux-mouse-content_2_ie5r15.png)

Agora vamos executar o arquivo no ***Terminal***;  
Será necessário acessar o ***Terminal*** e ir até o diretório onde salvou o script Bash. Uma forma simples de fazê-lo é acessando a pasta onde encontra-se o arquivo, clicar com o botão direito do mouse em uma área vazia da pasta e ir em ***Abrir no Terminal***;
![Img 03](https://res.cloudinary.com/k4bv734/image/upload/v1637846612/blog_content/linux-mouse-content_3_ele2vn.png)

No Terminal, primeiro vamos dar permissão de execução usando o comando:  
`chmod +x mousewheel.sh`  


Agora vamos executar o script:  
`sudo ./mousewheel.sh`


Será solicitada a senha root, digite-a e dê enter;

Se tudo correr bem, será apresentada a tela onde conseguirá definir a velocidade da rolagem do mouse. Indico definir em 3, porém fica a seu critério. Por fim clique em ***Apply***;
![Img 04](https://res.cloudinary.com/k4bv734/image/upload/v1637846612/blog_content/linux-mouse-content_4_jjidxt.png)

Pronto! Faça o teste e veja que a rolagem está bem mais ágil;  


Caso queira aumentar ou diminuir a rolagem, basta executar o script novamente;


Para aqueles que possuem mouse com botões extras além dos dois padrões e rolagem, caso encontrem algum problema nestes adicionais, tente adicionar ***-b "4 5"*** ao ***Imwheel***. No ***Terminal*** dê o comando:  
`imwheel -b "4 5"`

## Configurando o Imwheel para iniciar na reinicialização

Por padrão o Imwheel não irá carregar a configuração realizada a cada reinicio do sistema, tendo assim que fazer todo o procedimento novamente. Embora seja uma tarefa simples, é um trabalho adicional que precisamos contornar. 

Faça o seguinte:  
No ***Menu de aplicativos*** pesquise por ***aplicativos iniciais***;
![Img 05](https://res.cloudinary.com/k4bv734/image/upload/v1637846612/blog_content/linux-mouse-content_5_egj0sr.png)

Na próxima janela, clique em ***Adicionar***;


Digite no campo correspondente:  
* Nome = ***Imwheel***  
* Comando = ***selecione o arquivo .sh (mousewheel.sh)***  
* Comentário = ***Escreva o que quiser***  
![Img 06](https://res.cloudinary.com/k4bv734/image/upload/v1637846612/blog_content/linux-mouse-content_6_lwud0m.png)

* Clique em ***Adicionar*** e terá terminado as configurações.

## Manual
Para obter mais detalhes do Imwheel, digite no ***Terminal*** para acesso ao manual:  
`man imwheel`

## Fonte
> <https://dev.to/bbavouzet/ubuntu-20-04-mouse-scroll-wheel-speed-536o>  
> <https://io.bikegremlin.com/11541/linux-mouse-scroll-speed/>