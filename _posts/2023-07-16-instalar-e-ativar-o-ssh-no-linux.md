---
date: 2022-11-07 08:30:00
layout: post
title: Instalar e ativar o SSH no Linux
description: Instalar e ativar o SSH no Ubuntu
image: https://res.cloudinary.com/k4bv734/image/upload/v1689528618/ssh_nqfacu.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689528618/ssh_optimized_b8tlab.jpg
category: linux
tags:
  - ssh
  - linux
author: brunocosta
paginate: false
---
Utilizaremos no exemplo o Ubuntu.

Para instalar o SSH no Ubuntu Linux, siga os passos abaixo:

1. Abra o Terminal.

2. Execute o seguinte comando para instalar o servidor SSH:

   ```bash
   sudo apt install openssh-server
   ```

   Isso irá instalar o servidor SSH no seu sistema.

Para ativar o serviço do SSH no Ubuntu, siga as etapas abaixo:

1. No Terminal, execute o seguinte comando para verificar o status do serviço SSH:

   ```bash
   sudo service ssh status
   ```

   Isso irá exibir o status atual do serviço SSH. Para sair dessa visualização e retornar ao prompt do Terminal, pressione a tecla "q" para quit.

Para liberar as portas do SSH no Firewall UFW do Ubuntu Linux, execute o seguinte comando:

```bash
sudo ufw allow ssh
```

Dessa forma, as portas necessárias para o SSH serão liberadas no firewall UFW do Ubuntu. Isso permitirá que as conexões SSH sejam estabelecidas com o seu sistema.
