---
date: 2025-02-11 16:50:13
layout: post
title: Monitorando Eventos de Logon e Logoff no Log de Segurança do Windows
description: Com a crescente sofisticação das ameaças cibernéticas, torna-se
  essencial implementar mecanismos eficazes de monitoramento e controle de
  acessos. Neste post, abordamos como os eventos de Logon e Logoff no Log de
  Segurança do Windows (conhecido também como Visualizador de Eventos ou Windows
  Security Log), desempenham um papel crucial nesse processo.
category: servidores
tags:
  - servidores
  - windows
  - log
  - segurança
author: brunocosta
paginate: false
---
Com a crescente sofisticação das ameaças cibernéticas, torna-se essencial implementar mecanismos eficazes de monitoramento e controle de acessos. Neste post, abordamos como os eventos de Logon e Logoff no Log de Segurança do Windows (conhecido também como Visualizador de Eventos ou Windows Security Log), desempenham um papel crucial nesse processo.

### Diferença entre Autenticação e Logon

É importante entender a diferença entre autenticação e logon. A autenticação ocorre quando um usuário se identifica para obter acesso ao sistema, enquanto o evento de logon acompanha o momento em que o usuário efetivamente acessa um computador específico.
Independentemente do tipo de conta (local ou domínio) ou da sessão (interativa, via rede, RDP), o Windows gera um evento de logon no início e um evento de logoff ao término da sessão. Esses eventos são registrados pelas subcategorias "Logon" e "Logoff".

#﻿## Subcategorias de Logon/Logoff e suas Funções

O log de segurança do Windows classifica os eventos de logon em diferentes subcategorias, incluindo:
Logon: Registra a tentativa de logon e pode ser usado para correlacionar eventos associados à mesma sessão.
Logoff: Indica quando um usuário finaliza sua sessão, mas nem sempre está presente.
Account Lockout: Relacionado a contas bloqueadas devido a tentativas malsucedidas de login.
IPsec (Main Mode, Quick Mode, Extended Mode): Relacionado à segurança IP, estabelecendo conexões seguras entre dispositivos.
Special Logon: Indica logons administrativos ou privilegiados, facilitando a auditoria de acessos sensíveis.
Other Logon/Logoff Events: Inclui eventos como desbloqueio de tela, reconexões via Área de Trabalho Remota e trocas de credenciais.
Network Policy Server: Monitora autenticações via RADIUS e Network Access Protection (NAP), garantindo controle de acesso remoto seguro.

### Tipos de Logon e sua Importância

Diferentes tipos de logon podem indicar atividades distintas, sendo essenciais para uma análise mais detalhada:
Interativo: Quando um usuário acessa diretamente o dispositivo (login local ou console).
Rede: Quando um usuário se conecta a um recurso compartilhado na rede sem fazer login interativo.
Batch: Para execução de tarefas automatizadas, como scripts agendados.
Service: Utilizado por serviços do Windows que precisam rodar continuamente.
Remote Desktop (RDP): Indica conexões remotas ao sistema.
Unlock (Desbloqueio de Tela): Ocorre quando um usuário retorna de um bloqueio de tela.

#﻿## Principais Eventos de Logon e Logoff

1.Logon Bem-Sucedido (ID 4624)
Indica que um usuário autenticado acessou o sistema com sucesso. Esse evento contém informações como tipo de logon, nome de usuário, domínio e endereço IP de origem.
2.Falha no Logon (ID 4625)
Registra tentativas malsucedidas de logon, sendo útil para identificar ataques de força bruta ou tentativas de acesso não autorizado.
3.Logoff do Usuário (ID 4634)
Indica que uma sessão foi encerrada voluntariamente pelo usuário.
4.Encerramento de Sessão (ID 4647)
Ocorre quando um usuário faz logoff manualmente do sistema.
5.Bloqueio e Desbloqueio da Estação de Trabalho (IDs 4800 e 4801)
Permite rastrear quando um usuário bloqueia e desbloqueia a estação de trabalho, indicando períodos de inatividade.
6.Troca de Sessão e Conexões Remotas
ID 4778: Reconexão de sessão RDP.
ID 4779: Desconexão de sessão RDP.
ID 4776: Autenticação NTLM usada para acessar um recurso na rede.


#﻿## Como Monitorar Eventos de Logon/Logoff

Para visualizar esses eventos no Windows:
1.Abra o Visualizador de Eventos (eventvwr.msc).
2.Navegue até Logs do Windows > Segurança.
3.Use filtros para exibir eventos específicos (por ID ou usuário).

### Importância do Monitoramento

Detecção de acessos suspeitos: Identificar invasões ou tentativas de login mal-intencionadas.
Auditoria e conformidade: Empresas precisam manter registros de acessos para atender a regulamentações de segurança.
Gerenciamento de tempo e produtividade: Permite rastrear horários de entrada e saída dos usuários.
Cada evento de logon bem-sucedido gera um identificador único (Logon ID), que pode ser usado para correlacionar atividades específicas, como logoff e mudanças de credenciais dentro da mesma sessão.
Além disso, ao analisar logs de logon/logoff, administradores podem identificar comportamentos suspeitos, como:
Acessos fora do horário normal.
Múltiplas tentativas malsucedidas de login.
Uso excessivo de contas administrativas.
Logins simultâneos de um mesmo usuário em locais distintos.

#﻿## Conclusão

Ao configurar políticas de auditoria e monitoramento contínuo, as equipes de TI garantem mais segurança e controle sobre o ambiente de rede. Implementar alertas automáticos pode ser uma ótima estratégia para agir rapidamente diante de eventos suspeitos.