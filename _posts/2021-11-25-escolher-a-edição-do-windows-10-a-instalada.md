---
date: 2020-12-17 00:00:00
layout: post
title: Escolher a edição do Windows 10 a instalada
description: Como escolher a edição do Windows 10 a instalada quando as opções
  não são exibidas.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/edi%C3%A7%C3%A3o-windows-10_hld35w.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/edi%C3%A7%C3%A3o-windows-10_optimized_dodzrh.jpg
category: windows
tags:
  - windows10
author: brunocosta
paginate: false
---
Um problema que alguns tem encontrado no momento de fazer uma instalação limpa do Windows 10, é a não possibilidade de escolher a edição do sistema. Isso acontece pois a configuração do Windows considerar a edição da versão do sistema já ativada anteriormente no computador. Por exemplo: se você tem Windows 7 Home ativado a configuração do Windows irá automaticamente selecionar a edição principal do Windows 10 Home.
Para aqueles que o computador veio originalmente, por exemplo, com a edição Home do Windows 7/8/8.1 e no momento do lançamento do Windows 10 realizou a instalação forçada do Windows 10 Pro, você também terá a dificuldade listada acima, pois será detectada a chave do produto armazenada no BIOS que estará associada a edição do Windows na versão Home.
A solução será basicamente adicionar um arquivo "ei.cfg" na ISSO de instalação do Windows 10. Veja a seguir como:

1. Primeiro é necessário extrair a ISO do Windows 10 para adicionarmos o arquivo. Utilize o 7-Zip para tal tarefa 

2. Agora abra o Bloco de Notas (notepad.exe) e adicione o seguinte: 
[EditionID] 
Professional
[Channel]
Retail

3. Salve o arquivo como "ei.cfg". Utilize a aspas para evitar que o Bloco de notas salve o arquivo como ei.cfg.txt 

4. Abra novamente Bloco de Notas para criar o segundo arquivo pid.txt. Adicione o seguinte: 
[PID] 
Value=XXXXX-XXXXX-XXXXX-XXXXX-XXXXX

5. Substitua a sequência de X pela chave de licenciamento da sua versão 

6. Próximo passo será copiar estes arquivos e colar na pasta "Sources" dentro dos diretórios extraídos da ISSO do Windows 10 

7. Agora é só criar um pendrive bootável ou gravar em um DVD e rezlizar a instalação normalmente 

Observações adicionais: 

1. Caso você tenha uma versão OEM e não de varejo do Windows 10, o seu arquivo ei.cfg deverá conter o seguinte:
[EditionID] 
Enterprise
[Channel]
OEM
[VL]
0

2. Caso queira que apareça a opção de escolher a edição no momento da instalação, retire do seu arquivo ei.cfg as linhas: 
[EditionID] 
Professional

Deixe somente: 
[Channel] 
Retail
