---
date: 2022-09-07 08:30:00
layout: post
title: Forçar Sincronização do Active Directory Com Todos os Sites Remotos
description: Forçar Sincronização do Active Directory Com Todos os Sites Remotos
image: https://res.cloudinary.com/k4bv734/image/upload/v1689528617/replicacao-active-directory_nx2q9e.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689528617/replicacao-active-directory_optimized_oh5qqk.jpg
category: servidores
tags:
  - windowsserver
  - activedirectory
author: brunocosta
paginate: false
---

Um exemplo de como forçar a sincronização, utilizando o CMD ou PowerShell.

Para executar o comando a partir do AD Primário, siga as etapas abaixo no prompt de comando (como administrador):

```bash
repadmin /syncall /e /A /P /d /q
```

Aqui está uma descrição dos comandos utilizados:

- `/syncall`: sincroniza o Controlador de Domínio (DC) primário com todos os parceiros de replicação;
- `/e`: indica que a replicação será estendida a todos os sites remotos;
- `/A`: sincroniza todas as partições do servidor principal;
- `/P`: indica que as mudanças serão replicadas a partir do servidor primário;
- `/d`: identifica os servidores por seus nomes distintos em eventuais mensagens que possam aparecer;
- `/q`: não exibe as mensagens de status. Se você estiver executando o comando manualmente para solucionar algum problema, é recomendável não utilizar esse parâmetro para identificar possíveis erros.

