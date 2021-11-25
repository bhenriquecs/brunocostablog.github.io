---
date: 2020-12-17 00:00:00
layout: post
title: Pendrive bootável com Windows 10
description: Como criar um pendrive bootável com Windows 10.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/pendrive-boot-windows_dmud3f.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783288/blog/pendrive-boot-windows_optimized_v5fods.jpg
category: windows
tags:
  - windows
  - instalação
  - boot
author: brunocosta
paginate: false
---
## Criando o pendrive com Windows 10

Faça o download do **Windows 10**, caso não o tenha ou queira a versão mais atualizada:  
<https://www.microsoft.com/pt-br/software-download/windows10>


Escolha a opção x64, pois esta que funciona no modo **UEFI** e depois selecione baixar em formato **.iso**;


Conecte o pendrive ao PC;


Após o download, abra o ***PowerShell*** como administrador e dê os comandos (**um de cada vez**):
```
diskpart
list disk (anote o número que seja referente ao pendrive)
sel disk x (x é o número do pendrive)
clean
convert gpt
create partition primary
format fs=fat32 quick
assign
```

Lembre-se de dar Enter após cada comando! 


Faça a extração da **.iso** do Windows. Você pode utilizar o 7-Zip ou WinRAR para tal tarefa;


Copie e cole todos os arquivos extraídos no pendrive;


Agora conecte esse pendrive no PC a ser formatado e acesse o setup;


Em alguns modelos será necessário desativar o ***"secure boot"***. Faça-o;


Nas opções de boot, selecione o modo UEFI e, se tiver a opção, selecione o pendrive como a primeira opção para o boot. Reinicie;


Se tudo estiver certo, após o reinicio, agora você está na tela de instalação do Windows. Prossiga com a instalação do sistema operacional normalmente.

## Erro na formatação/instalação: partição MBR
Para aqueles que ao tentar instalar o Windows tiveram a mensagem "o disco selecionado está no estilo da partição MBR" ou algo do tipo, faça o seguinte para resolver:


Na primeira tela após iniciar o pendrive bootável com o Windows, pressione ***SHIFT + F10***;


O Prompt de Comando será aberto, então dê os comandos :
```
diskpart 
list disk
sel disk x (substitua x pelo número do seu HD ou SSD)
clean (irá deletar todos os dados do disco, tenha o backup se necessário)
convert gpt
create partition primary
format fs=ntfs
exit
exit

```

Agora prossiga com a instalação do sistema operacional normalmente.