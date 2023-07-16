---
date: 2022-08-07 08:30:00
layout: post
title: Comando Vi/Vim básicos
description: Comando Vi/Vim básicos
image: https://res.cloudinary.com/k4bv734/image/upload/v1689528617/vim_dqjosf.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689528617/vim_optimized_cd1p6m.jpg
category: linux
tags:
  - editor
author: brunocosta
paginate: false
---
Aqui estão alguns dos comandos básicos do editor de texto Vi/Vim, amplamente utilizado no mundo Unix/Linux:

**Abrindo o editor**
```
vi
```
Comando para abrir o Vi vazio, sem exibir um arquivo.

**Abrindo um arquivo**
```
vi nome-do-arquivo
```
Abre o arquivo "nome-do-arquivo" existente no diretório atual.

```
vi /home/bruno/nome-do-arquivo
```
Abre o arquivo existente em outro local diferente do diretório atual.

**Movimentando pelo texto**
- `H`: Move para a primeira linha, topo da tela.
- `j`: Move para a próxima linha, linha abaixo.
- `k`: Move para a linha anterior, linha acima.
- `l`: Move para a direita.
- `h`: Move para a esquerda.
- `L`: Move para a última linha, fim da tela.
- `G`: Move para a última linha do arquivo.
- `0`: Move para o início da linha atual.
- `$`: Move para o final da linha atual.
- `nG`: Move para a linha n, onde n é o número da linha.
- `Ctrl + f`: Move para a próxima tela.
- `Ctrl + b`: Move para a tela anterior.

**Editando o texto**
Após abrir o arquivo, para entrar no modo de edição, utilize o comando abaixo:
- `i`: Insere à esquerda, então movimente o cursor para onde deseja realizar a edição.
- `R-Enter`: Quebra de linha.
- `J`: Une a linha atual com a próxima.
- `u`: Desfaz o comando anterior.
- `x`: Apaga um caractere.
- `dw`: Apaga uma palavra.
- `dd`: Apaga uma linha.
- `yy`: Copia uma linha.
- `P`: Cola a linha copiada acima.
- `p`: Cola a linha copiada abaixo.

**Buscando texto**
- `/palavra`: Procura a palavra em todo o texto do arquivo.
- `?palavra`: Move para a ocorrência anterior da palavra.
- `n`: Procura a próxima ocorrência do comando `/` ou `?` descritos acima.

**Salvar e Sair do editor Vi**
- `:w`: Salva o arquivo.
- `:w novo_arquivo`: Salva o arquivo com um novo nome.
- `:wq`: Salva e sai do editor.
- `:q`: Sai do editor.
- `:q!`: Sai do editor sem salvar.
