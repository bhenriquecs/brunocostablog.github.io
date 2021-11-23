---
date: 2021-12-31T13:48:05.000Z
layout: post
title: Apache + PHP + MySQL no Windows
subtitle: 'Como montar um servidor web com Apache com suporte ao PHP e MySQL sem usar pacotes prontos como o WAMP e XAMP?'
description: >-
  Como montar um servidor web com Apache com suporte ao PHP e MySQL sem usar pacotes prontos como o WAMP e XAMP?
image: >-
  https://res.cloudinary.com/k4bv734/image/upload/v1637696792/blog/apache_aqldc8.jpg
optimized_image: >-
  https://res.cloudinary.com/k4bv734/image/upload/v1637696792/blog/apache_optimized_a0make.jpg
category: servidores
tags:
  - webserver
  - servidorweb
  - apache
  - mysql
  - PHP
author: brunocosta
paginate: true
---
Aqui iremos tratar somente as instalações e configurações iniciais para funcionamento padrão, não entraremos nas demais configurações que cada ferramenta possui.  
Antes de tudo, recomendo a leitura das documentações oficiais de cada ferramenta/solução:

> Apache: <a href="http://httpd.apache.org/docs/current/platform/windows.html">http://httpd.apache.org/docs/current/platform/windows.html</a>  
> PHP: <a href="https://www.php.net/manual/en/index.php">https://www.php.net/manual/en/index.php</a>  
> MySQL: <a href="https://dev.mysql.com/doc">https://dev.mysql.com/doc</a>

## Apache

O Apache não fornece binários para Windows, porém existem várias opções de terceiros disponíveis para download, como por exemplo o Apache Lounge e Apache Haus.  
Baixe a versão correta para o seu sistema operacional, x86 (32 bits) ou x64 (64 bits):

> 32 bits: <a href="https://www.apachelounge.com/download/VS16/binaries/httpd-2.4.46-win32-VS16.zip">https://www.apachelounge.com/download/VS16/binaries/httpd-2.4.46-win32-VS16.zip</a>  
> 64 bits: <a href="https://www.apachelounge.com/download/VS16/binaries/httpd-2.4.46-win64-VS16.zip">https://www.apachelounge.com/download/VS16/binaries/httpd-2.4.46-win64-VS16.zip</a>

Baixe e instale também o Visual C ++ Redistributable para Visual Studio 2015-2019, caso seu sistema não o tenha. Também escolha a versão apropriada.

> 32 bits: <a href="https://aka.ms/vs/16/release/VC_redist.x86.exe">https://aka.ms/vs/16/release/VC_redist.x86.exe</a>  
> 64 bits: <a href="https://aka.ms/vs/16/release/VC_redist.x64.exe">https://aka.ms/vs/16/release/VC_redist.x64.exe</a>

Descompacte o apache baixado na raiz do seu disco (geralmente C:\). Você terá algo como C:\Apache24\ .  
Abra o CMD (Prompt de comando) e vá até o diretório ***C:\Apache24\bin*** .
Execute:
```
httpd.exe
```

O firewall do Windows pode pedir permissão para o Apache se comunique em específicas redes. Sugiro aceitar em redes domésticas e corporativas e não permitir em redes públicas.  
O Apache já está instalado. Para conferir abra um navegador e acesse ***http://localhost***. Se aparecer a página com os dizeres ***"It Works!"*** significa que o Apache está funcionando corretamente.  
Caso receba algum aviso sobre "não poder determinar o nome do domínio totalmente qualificado", faça o seguinte:
* Com um editor de texto, abra o arquivo httpd.conf, existente no diretório C:\Apache24\conf
* Encontre ***ServerName <yourhostname>***. Descomente e altere ***<yourhostname>*** por ***<localhost>*** ou pelo ***<nome do host>*** do sistema
* Salve o arquivo

Para executar o Apache automaticamente sempre que o sistema for iniciado, sem a necessidade de fazer login ou executar o serviço manualmente, vamos transformá-lo em um serviço do Windows.
* Abra o CMD como administrador (caso tenha o fechado)
* Vá até o diretório C:\Apache24\bin
* Dê o comando:
```
httpd.exe -k install
```

Pronto! Agora você tem o Apache instalado como serviço do Windows o qual poderá gerenciar no Serviços (services.msc).

## PHP



HTML defines a long list of available inline tags, a complete list of which can be found on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

* **To bold text**, use `<strong>`.
* *To italicize text*, use `<em>`.
* Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
* Citations, like <cite>&mdash; Thiago Rossener</cite>, should use `<cite>`.
* <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
* Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

--page-break--

## Code

Cum sociis natoque penatibus et magnis dis `code element` montes, nascetur ridiculus mus.

```js
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
```

Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa.

## Lists

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.

* Praesent commodo cursus magna, vel scelerisque nisl consectetur et.
* Donec id elit non mi porta gravida at eget metus.
* Nulla vitae elit libero, a pharetra augue.

Donec ullamcorper nulla non metus auctor fringilla. Nulla vitae elit libero, a pharetra augue.

1. Vestibulum id ligula porta felis euismod semper.
2. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
3. Maecenas sed diam eget risus varius blandit sit amet non magna.

Cras mattis consectetur purus sit amet fermentum. Sed posuere consectetur est at lobortis.

Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Nullam quis risus eget urna mollis ornare vel eu leo.

## Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](https://placehold.it/800x400 "Large example image") ![placeholder](https://placehold.it/400x200 "Medium example image") ![placeholder](https://placehold.it/200x200 "Small example image")

## Tables

Aenean lacinia bibendum nulla sed consectetur. Lorem ipsum dolor sit amet, consectetur adipiscing elit.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Upvotes</th>
      <th>Downvotes</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>21</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Charlie</td>
      <td>7</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.
