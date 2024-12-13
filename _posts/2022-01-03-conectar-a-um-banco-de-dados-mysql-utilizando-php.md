---
date: 2022-01-03 15:11:20
layout: post
title: Conectar a um banco de dados MySQL utilizando PHP
description: Como conectar a um banco de dados MySQL utilizando PHP atráves das
  bibliotecas MySQLi e PDO
image: https://res.cloudinary.com/k4bv734/image/upload/v1641232056/blog/php_g3jvp0.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1641232056/blog/php_optimized_gnbp7p.jpg
category: desenvolvimento
tags:
  - php
  - mysql
  - mysqli
  - pdo
author: brunocosta
paginate: false
---
Existem duas formas principais de se conectar a um banco de dados MySQL usando o PHP: utilizando as bibliotecas **MySQLi** e **PDO**.

**MySQLi** (MySQL Improved) é uma extensão exclusiva para o MySQL e oferece interface tanto procedural quanto orientada a objetos.

**PDO** (PHP Data Object) é orientado a objetos e suporta, além do MySQL, banco de dados distintos, como, por exemplo, o MSSQL e PostgreSQL.

## Usando MySQLi

Primeiro, no ***php.ini***, ative a seguinte extensão:

`extension=php_mysqli.dll`

Para ativar uma extensão, basta retirar o "**;**" (ponto e vírgula) do início da linha, salvar o arquivo e reiniciar seu servidor web (Apache, IIS, Nginx, etc).

No editor de texto/código de sua preferência, crie um novo arquivo nomeado como "*connect.php*".

Copie e cole o código abaixo no arquivo recém criado:
```php
<?php
$servername = "localhost";
$database = "nomedobancodedados";
$username = "usuario";
$password = "senha";

# Cria a conexão
$conn = mysqli_connect($servername, $username, $password, $database);

# Verifica a conexão
if (!$conn) {
    die("A conexão falhou: " . mysqli_connect_error());
}
echo "Conectado com sucesso!";
mysqli_close($conn);
?>
```
No código, altere os valores das variáveis para os dados do seu servidor e credencias do banco de dados.

**NOTA:** esses dados ficam dentro das aspas, não as excluam.

Salve o arquivo.

### Explicação do código utilizado (extensão MySQLi)

* *mysqli_connect()* é uma função interna do PHP que estabelece uma nova conexão com um servidor MySQL;
* As variáveis *$servername*, *$database*, *$username*, e *$password* receberão os dados referentes ao servidor e banco. Esses dados serão passados para a função citada acima;
* Se por algum (ou vários) motivo a conexão não for bem sucedida, a função *die()* é executada, o script é encerrado e a mensagem "*A conexão falhou...*" é exibida;
* Se correr tudo bem com a conexão, será exibida a mensagem "*Conectado com sucesso!*";
* Por fim, a função *mysqli_close()* fecha a conexão aberta anteriormente com o banco de dados.

## Usando PDO

Primeiramente ative as seguintes extensões no php.ini:
`extension=pdo_firebird`  
`extension=pdo_mysql`  
`extension=pdo_oci`  
`extension=pdo_odbc`  
`extension=pdo_pgsql`  
`extension=pdo_sqlite`  

Para ativar basta retirar o ";" (ponto e vírgula) do início das linhas, salvar o arquivo e reiniciar seu servidor web (Apache, IIS, Nginx, etc).

No editor de texto/código de sua preferência, crie um novo arquivo nomeado como "*config.php*".

Copie e cole o código abaixo e altere os valores das variáveis com o dados referentes ao banco de dados:
```php
<?php
$host = 'localhost';
$dbname = 'nomedobancodedados';
$username = 'usuario';
$password = 'senha';
?>
```
Salve o arquivo.

Crie outro arquivo chamado "*connect.php*", copie e cole o código abaixo:
```php
<?php
require_once 'pdoconfig.php';
try {
   $conn = new PDO("mysql:host=$host;dbname=$dbname", $username, $password);
   echo "Conectado a $dbname em $host com sucesso.";
} catch (PDOException $pe) {
   die("Não foi possível se conectar ao banco de dados $dbname :" . $pe->getMessage());
}
?>
```
### Explicação do código utilizado (extensão PDO)

* No primeiro arquivo, é definido as variáveis com os dados do servidor de banco de dados;
* No arquivo *connect.php*, iniciamos requerendo o arquivo *config.php* para termos acesso aos dados das variáveis definidos anteriormente;
* Em *try*, teremos a string DSN (Data Source Name) que tem como função passar os parâmetros de configuração para a biblioteca PDO e assim iniciar a tentativa de conexão;
* Caso a conexão ocorra com sucesso, a mensagem "*Conectado a $dbname em $host com sucesso.*" será exibida;
* Em caso de erro na conexão, o bloco *catch* é executado e a mensagem "*Não foi possível se conectar ao banco de dados $dbname :...*" é mostrada.