---
date: 2022-05-07 08:30:35
layout: post
title: Verificar se porta está aberta em um servidor/estação da rede
description: Verificar se porta está aberta em um servidor/estação da rede
image: https://res.cloudinary.com/k4bv734/image/upload/v1689528618/windows-server_wpeif3.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1689528618/windows-server_optimized_xnefrs.jpg
category: windows
tags:
  - windowsserver
  - portas
author: brunocosta
paginate: false
---
Existem diversas ferramentas e métodos disponíveis para testar remotamente se as portas estão abertas em um servidor. Aqui estão duas opções comuns:

**Telnet**: O Telnet é uma ferramenta de linha de comando que permite estabelecer uma conexão com um host remoto em uma porta específica. No entanto, o Telnet não está habilitado por padrão no Windows 10 e no Windows Server 2019, então você precisará ativá-lo nas configurações do Windows.

Para testar uma porta usando o Telnet, você pode utilizar o seguinte comando:

```bash
telnet <endereço IP ou nome do host> <porta>
```

Por exemplo, para testar a porta 80 (HTTP), você pode usar:

```bash
telnet www.example.com 80
```

Se a porta estiver aberta, você verá uma tela em branco ou uma mensagem de boas-vindas. Caso contrário, você receberá um erro ou uma mensagem de falha na conexão.

**PowerShell**: O PowerShell oferece cmdlets que permitem verificar o status de uma porta em um servidor remoto. Um cmdlet útil é o Test-NetConnection, que pode ser utilizado para testar a conectividade em uma porta específica.

Para testar uma porta usando o Test-NetConnection, você pode executar o seguinte comando no PowerShell:

```bash
Test-NetConnection -ComputerName <endereço IP ou nome do host> -Port <porta>
```

Por exemplo, para testar a porta 80 (HTTP), você pode usar:

```bash
Test-NetConnection -ComputerName www.example.com -Port 80
```

O comando retornará informações sobre o status da porta, incluindo se ela está aberta ou fechada.

Essas são apenas duas opções para testar a conectividade de portas remotamente. Existem outras ferramentas disponíveis, como o Nmap, que oferecem recursos avançados de varredura de portas. Escolha o método que melhor se adequa às suas necessidades e às ferramentas disponíveis em seu ambiente.