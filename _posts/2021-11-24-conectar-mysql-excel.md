---
date: 2021-03-05 12:00:00
layout: post
title: Conectar banco de dados MySQL ao Excel
subtitle: ""
description: Conectar banco de dados MySQL ao Excel
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/excel-mysql_i1tdnc.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/excel-mysql_optimized_dxgzt5.jpg
category: bancodedados
tags:
  - mysql
  - excel
  - sql
  - odbc
author: brunocosta
paginate: false
---
Para algumas situações onde precisamos resgatar informações existentes em um sistema que faz uso de banco de dados MySQL e desejamos tratar em uma planilha Excel, é interessante utilizar um recurso, que não é nativo, para automatizar tal tarefa. Neste caso é a conexão de banco de dados MySQL diretamente ao Excel.  

Abaixo como iremos proceder:  

Baixe o conector ODBC:

> [https://dev.mysql.com/downloads/connector/odbc](https://dev.mysql.com/downloads/connector/odbc)

Ele é basicamente uma interface que permite que linguagens de programação que o suportam se comuniquem com um banco de dados MySQL;

**Dica:** ao clicar em ***"Download"*** será carregada uma nova página solicitando login com uma conta free. Não é necessário realizar esse cadastro ou login, somente clique em ***"No thanks, just start my download."*** que é exibido abaixo;

Instale o programa, selecionando a instalação completa (isso é uma sugestão, fica a seu critério);

Após a instalação, pesquise no ***Menu Iniciar*** pelo termo ***ODBC*** e abra o ***"Fonte de dados ODBC (xx bits)"*** ou abra o ***Painel de Controle***, acesse ***Ferramentas Administrativas*** e abra o ***"Fonte de dados ODBC (xx bits)"***;

Na janela de ***Administração de Fonte Dados ODBC***, clique em ***Adicionar***;
![Img 01](https://res.cloudinary.com/k4bv734/image/upload/v1637785041/blog_content/excel-mysql-content_1_tnwbmb.png)

Na próxima janela selecione ***MySQL ODBC x.x Driver***, o ***x.x*** será conforme a versão instalada, e clique em ***Concluir***;
![Img 02](https://res.cloudinary.com/k4bv734/image/upload/v1637785042/blog_content/excel-mysql-content_2_w62c9k.png)

Preencha conforme os dados de acesso ao seu banco de dados;
![Img 03](https://res.cloudinary.com/k4bv734/image/upload/v1637785041/blog_content/excel-mysql-content_3_x8v9kh.png)


Clique em ***Test*** para testar a conexão. Caso esteja tudo OK, irá aparecer ***Connection successful***. Clique em ***OK*** para confirmar a configuração e feche todas as janelas abertas;

Agora abra o Excel e vá em ***Dados > Conexões Existentes***. Na janela que se abre, clique em ***Procurar Mais...***;
![Img 04](https://res.cloudinary.com/k4bv734/image/upload/v1637785042/blog_content/excel-mysql-content_4_rpi61u.png)
	
Agora clique em ***Nova fonte de dados...***;
![Img 05](https://res.cloudinary.com/k4bv734/image/upload/v1637785042/blog_content/excel-mysql-content_5_t06f1q.png)
	
Selecione ***DSN ODBC*** e clique em ***Avançar***;

Após selecione a conexão criada anteriormente e clique em ***Avançar***;

Na próxima tela, selecione o banco desejado e, se desejado, selecione uma tabela específica para conectar. Sugiro que desmarque essa caixa, pois podemos tratar isso em uma query SQL;

Clique em ***Avançar***. Na próxima tela, serão exibidas informações da nova conexão. Pode deixar como está e clique em ***Concluir***;

Irá aparecer uma nova tela para seleção de tabelas. Selecione a(s) tabela(s) desejada(s) para prosseguirmos. Será possível editar posteriormente via query SQL;

Agora clique em ***Dados > Conexões***. Na janela exibida terá a conexão criada. Clique em ***Propriedades***;
![Img 06](https://res.cloudinary.com/k4bv734/image/upload/v1637785042/blog_content/excel-mysql-content_6_ofzsq5.png)

Na próxima tela selecione a aba ***Definição***. No campo ***Texto do comando*** é onde você irá fazer a sua query SQL desejada. Depois é só clicar em ***OK*** que a consulta será realizada e apresentada na planilha;
![Img 07](https://res.cloudinary.com/k4bv734/image/upload/v1637785042/blog_content/excel-mysql-content_7_bg9zk4.png)

Os dados serão carregados na planilha conforme as condições da sua query e já poderá começar a tratar os dados conforme a necessidade.