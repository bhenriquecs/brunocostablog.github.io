---
date: 2026-10-21 19:00:28
layout: post
title: "Seu site ou sistema pode estar em perigo: o que fazer com a falha grave
  do PHP"
subtitle: "Nesta quarta-feira, 21 de outubro de 2026, foi publicada uma falha
  grave no PHP. PHP é o motor que faz funcionar uma parte enorme dos sites e
  sistemas na internet: sites institucionais, blogs, lojas virtuais, áreas do
  cliente, intranets e sistemas feitos sob medida."
description: "Nesta quarta-feira, 21 de outubro de 2026, foi publicada uma falha
  grave no PHP. PHP é o motor que faz funcionar uma parte enorme dos sites e
  sistemas na internet: sites institucionais, blogs, lojas virtuais, áreas do
  cliente, intranets e sistemas feitos sob medida."
image: https://res.cloudinary.com/k4bv734/image/upload/v1792621018/blog/Vulnerabilidade_Cr%C3%ADtica_no_PHP_v7yljk.png
category: ciberseguranca
tags:
  - php
  - segurança
  - cibersegurança
  - vulnerabilidade
author: brunocosta
paginate: false
---
<!--StartFragment-->

A falha permite que uma pessoa de fora, sem senha, mande o servidor executar comandos. Na prática, isso pode significar site alterado, dados de clientes copiados, envio de spam a partir da sua empresa ou o servidor usado para atacar outras pessoas. O problema recebeu o apelido de php2shell. Os códigos oficiais são CVE-2026-109618 e CVE-2026-109619.

Órgãos de segurança dos Estados Unidos e da União Europeia pediram atualização imediata. Há relatos de varreduras e tentativas de ataque já no dia da divulgação. Quem tem site ou sistema no ar precisa agir hoje, mesmo sem equipe técnica dentro de casa.

![](https://res.cloudinary.com/k4bv734/image/upload/v1792620020/blog_content/falha_grave_PHP_qrg5v7.png)

## Isso vale para a minha empresa?

Vale a pena tratar como sim até alguém confirmar o contrário, se a empresa tem algum destes:

* site em WordPress, loja virtual ou página com formulário e área restrita;
* sistema interno, portal de clientes ou intranet acessível pela internet;
* site ou sistema em hospedagem, em nuvem ou num servidor da própria empresa;
* mais de um endereço (o site público e um “sistema antigo” que quase ninguém usa).

Muita gente nunca instalou PHP e mesmo assim depende dele. A hospedagem ou quem criou o site instalou esse motor por baixo. Atualizar texto, tema, plugin ou o layout não troca esse motor.

Também entra software que usa PHP escondido, como alguns painéis e sistemas prontos. Se você não sabe o que sustenta o site, a pergunta certa para quem hospeda é simples: “Esse ambiente roda PHP? Já foi atualizado hoje?”

Um site montado em plataforma fechada, daquelas em que você só edita o conteúdo e o fornecedor cuida do servidor, tende a ser corrigido por eles. Ainda assim, vale confirmar por escrito.

## Por que a senha do site não resolve

O furo está no motor, não na tela de login. Em muitos servidores, o ataque acontece antes de o site em si começar a funcionar. Senha forte, plugin de segurança e o fato de “quase ninguém conhecer o endereço” não fecham essa porta.

O site de testes, a hospedagem antiga e o sistema que “só o financeiro usa” também contam, se estiverem acessíveis de fora.

## O que fazer hoje

Você não precisa corrigir isso sozinho. Precisa colocar a tarefa na mão de quem administra a hospedagem ou o servidor, com um pedido claro.

Se existe uma empresa, um freelancer ou um setor de TI cuidando do ambiente, encaminhe o recado abaixo e peça retorno ainda hoje, com a versão do PHP que ficou valendo.

Se o site está numa hospedagem compartilhada, quem atualiza o PHP é a própria hospedagem, ou o painel permite trocar a versão. Abra um chamado com o mesmo texto.

Se ninguém mais cuida do site, porque quem desenvolveu saiu ou o contrato acabou, o caminho é chamar alguém para localizar onde o site está, pedir a atualização e testar se formulário, login e pagamentos continuam funcionando. A [BHCS Solutions](https://bhcs.solutions/) faz esse tipo de atendimento para empresas que têm site ou sistema e não têm equipe de TI: primeiro mapeamos o que está no ar, depois a correção com quem hospeda o ambiente.

Se a resposta for “não conseguimos atualizar agora”, o mais seguro é tirar o site ou o sistema da internet até a correção. Deixar no ar “só até segunda” é manter a porta aberta. Isso pesa ainda mais quando o PHP é antigo (versões 8.1, 7 ou anteriores), porque muitas delas não recebem mais correção oficial.

## Quando chamar ajuda além da atualização

Procure quem cuida do ambiente, ou um parceiro de confiança, se aparecer algo fora do normal perto desta data: site diferente do que você publicou, aviso de antivírus, clientes recebendo e-mail estranho em nome da empresa, ou a hospedagem falando em invasão.

Nesse caso, a prioridade é conter o dano e entender se dados de clientes foram acessados. Só recolocar o site no ar repete o risco.

Empresas com mais de um site, um sistema antigo e uma hospedagem contratada há anos costumam não ter essa lista na mão. Levantar o que existe, cobrar a atualização de quem hospeda e conferir se o negócio voltou ao normal é um trabalho curto, e é exatamente o tipo de situação em que a [BHCS Solutions](https://bhcs.solutions/seguranca) entra como parceira. Entre em contato conosco: [contato@bhcs.solutions](mailto:contato@bhcs.solutions) ou +55 [(31) 2888-1877](https://wa.me/553128881877?text=Ol%C3%A1%21%20Vim%20pelo%20site%20da%20BHCS%20Solutions%20e%20gostaria%20de%20conversar.) (Tel./Whatsapp).

<!--EndFragment-->