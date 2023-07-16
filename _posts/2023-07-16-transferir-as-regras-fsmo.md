---
date: 2022-07-07 08:30:00
layout: post
title: Transferir as regras FSMO
description: Transferir as regras FSMO
image: https://res.cloudinary.com/k4bv734/image/upload/v1689528618/fsmo_levdey.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689528618/fsmo_optimized_mxtofk.jpg
category: servidores
tags:
  - windowsserver
  - fsmo
  - activedirectory
  - ad
author: brunocosta
paginate: false
---
Para preparar a transferência das funções do Active Directory, siga as etapas abaixo:

1. Verifique qual servidor contém as 5 regras de operações do Active Directory. No prompt de comando (CMD), execute o seguinte comando:

   ```bash
   netdom query fmso
   ```

   Será exibido o servidor que contém as regras.

2. Antes de transferir as funções, é necessário preparar o domínio. No servidor que receberá as regras, insira o DVD do Windows Server (x = versão do sistema instalado).

3. Abra o CMD com privilégios de administrador e navegue até o seguinte caminho: DVD > support > adprep.

4. No diretório acima, execute os seguintes comandos:

   ```bash
   adprep.exe /forestprep
   ```

   Pressione "C" e "ENTER" para confirmar que as informações de toda a floresta foram atualizadas.

   ```bash
   adprep.exe /domainprep
   ```

   Verifique se as informações de todo o domínio foram atualizadas.

   ```bash
   adprep.exe /rodcprep
   ```

   Verifique se o Rodprep foi concluído com êxito.

   ```bash
   adprep.exe /domainprep /gpprep
   ```

   Verifique se as atualizações de GPO não são necessárias, pois já foram realizadas.

5. Após preparar o domínio, é hora de transferir as funções. Acesse o servidor que contém as regras FMSO e abra o CMD como administrador.

6. Execute os seguintes comandos:

   ```bash
   ntdsutil
   roles
   connections
   connect to server SERVER
   ```

   Substitua "SERVER" pelo nome do servidor que receberá as funções.

7. Em seguida, execute os comandos de transferência para cada uma das funções:

   ```bash
   transfer schema master
   ```

   Confirme a transferência clicando em "Sim".

   ```bash
   transfer PDC
   ```

   Clique em "Sim" para confirmar.

   ```bash
   transfer naming master
   ```

   Confirme clicando em "Sim".

   ```bash
   transfer RID master
   ```

   Clique em "Sim" para confirmar.

   ```bash
   transfer infrastructure master
   ```

   Novamente, clique em "Sim" para confirmar.

8. Após a transferência das funções, para confirmar se todas foram transferidas com sucesso, saia do ntdsutil (ou abra outro CMD) e execute o comando:

   ```bash
   netdom query fmso
   ```

   Será exibido o status das funções FMSO.
