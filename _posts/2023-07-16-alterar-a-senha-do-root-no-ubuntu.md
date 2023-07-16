---
date: 2022-06-07 08:30:00
layout: post
title: Alterar a senha do root no Ubuntu
description: Alterar a senha do root no Ubuntu
image: https://res.cloudinary.com/k4bv734/image/upload/v1689528617/user-root-ubuntu_g8mpzo.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689528617/user-root-ubuntu_optimized_ndeg1k.jpg
category: linux
tags:
  - linux
  - root
author: brunocosta
paginate: false
---
O usuário root (ou superusuário) é uma conta especial presente em todos os sistemas Linux e Unix, que possui acesso total a todos os comandos e recursos do sistema, sem restrições.
No Ubuntu, os usuários são incentivados a realizar tarefas administrativas concedendo privilégios de sudo a usuários regulares. Isso permite que usuários autorizados executem programas como outro usuário, geralmente o root.

O usuário inicial criado durante a instalação do Ubuntu já é membro do grupo sudo, o que significa que provavelmente o usuário com o qual você fez login já possui privilégios administrativos.

Caso haja a necessidade de habilitar a conta root, é possível fazê-lo definindo uma senha para o usuário root.

Para alterar a senha do usuário root no Ubuntu, execute o seguinte comando utilizando um usuário com privilégios de sudo:

```bash
sudo passwd root
```

Isso permitirá que você defina uma nova senha para o usuário root.
