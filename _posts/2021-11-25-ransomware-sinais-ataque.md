---
date: 2020-12-19 00:00:00
layout: post
title: "Ransomware: alguns sinais de que está prestes a ser atacado"
description: Geralmente em uma ataque Ransomware, o atacante/invasor utiliza
  ferramentas legítimas para preparar o terreno antes do ataque.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/ramsonware-cuidados_i3eahv.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/ramsonware-cuidados_optimized_fjh58f.jpg
category: ciberseguranca
tags:
  - cibersegurança
  - ransomware
  - cybersecurity
author: brunocosta
paginate: false
---
Geralmente em um ataque Ransomware, o atacante/invasor utiliza ferramentas legítimas para preparar o terreno antes do ataque. O sujeito(s) já terá acesso a rede da vítima. Os métodos que permitirão a invasão explicarei em outro post, mas comumente são via arquivos maliciosos enviados por e-mail ou via algum drive em nuvem e executados por usuários com pouca instrução tecnológica. Utilizam também de artifícios da engenharia social, entre outros meios.

Com o sucesso no acesso a rede, listarei abaixo alguns indicadores de que estão vasculhando sua rede em busca de brechas para execução do script malicioso:

* #### Um Scanner de rede, principalmente em um servidor
Caso encontre algum software do tipo em seus servidores e este não foi, obviamente, instalado por você ou algum administrador da rede, desconfie, pois provavelmente está sob ataque. O invasor coletará todo tipo de informação relevante, deste o nome do domino, contas com acesso administrador e arquivos que poderão acessar. Exemplos de scanners existentes: Advanced Port Scanner, AngryIP. 


* #### Ferramentas que possibilita a desativação do software antimalware (o chamado antivírus)
Após os invasores conseguirem o acesso de administrador, geralmente tentarão desabilitar o software de proteção utilizando programas que ajudam na remoção forçada do software. Poderão utilizar softwares legítimos como o IOBit Unistaller, PC Hunter, Process Hacker, entre outros. Caso a equipe de tecnologia e nem você tenha realizado a instalação deste tipo de software, está na hora de questionar e investigar sobre.


* #### A existência de MimiKatz
A detecção de MimiKatz em qualquer local deve ser investigada. Este tipo de ferramenta é amplamente utilizada para roubo de credenciais. Os invasores também utilizam o Microsoft Process Explorer, este está incluído no Windows Sysinternals, uma ferramenta legítima que pode despejar o LSASS.exe da memória, criando um arquivo .dmp. Após, poderão então levar isso para seu próprio ambiente e usar o MimiKatz para extrair com segurança nomes de usuário e senhas.


* #### Padrões de comportamento suspeitos
Detecções que ocorrem de maneira padronizada, de forma constantes, repetidas e diárias geralmente é indicação de que algo anormal está acontecendo. Todos os responsáveis pela rede devem se perguntar o por que está acontecendo continuamente tal situação. Sempre acompanhe e investigue os alertas da sua solução de segurança e logs do sistema.


* #### Tentativas de acesso a servidor de Área de Trabalho Remota
Caso sua operação necessite de ter um servidor RDP, o que não é o ideal (pensando na segurança opte por uma VPN, mas iremos tratar deste assunto em outro post), é de suma importância verificar constantemente os logs do sistema e do seu software de segurança. Nos servidores Windows utilize o Visualizador de Eventos (eventvwr.msc) para analisar os acessos e tentativas de acesso ao servidor (para isso ative a auditoria). Caso o atacante obtenha sucesso no acesso, provavelmente você irá encontrar algumas das situações citadas nos tópicos 1, 2 ou 3 deste post.


* #### Ataques de testes
Os invasores podem implantar pequenos ataques em alguns computadores da rede para avaliar o método de implantação do script malicioso ocorre com êxito. Sempre mantenham o parque de computadores, não somente os servidores mas também as estações de trabalho, atualizadas e com o software de segurança em dia. Além disso, tenha uma política de segurança bem definida e amplamente divulgada.



Bem, esses são alguns sinais e dicas a se observar em segurança, para evitarmos, assim, um ataque bem sucedido de Ransomware.