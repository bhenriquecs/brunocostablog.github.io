---
date: 2020-12-17 00:00:00
layout: post
title: File Server - Auditoria arquivos excluídos
description: Arquivos deletados através do mapeamento de rede (Pasta
  Compartilhada), diferentemente dos excluídos localmente, não são enviados para
  a lixeira.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/fileserver_hpbn4y.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637783286/blog/fileserver_optimized_hooyd9.jpg
category: servidores
tags:
  - fileserver
  - auditoria
  - arquivos
author: brunocosta
paginate: false
---
Arquivos deletados através do mapeamento de rede (Pasta Compartilhada), diferentemente dos excluídos localmente, não são enviados para a ***lixeira***. Funciona como quando utilizamos a combinação Shift + Del. Para recuperação devemos recorrer aos nossos backups ou, para aqueles que são imprudentes com os backups, utilizar algum software de recuperação (que nem sempre têm o resultado desejado).

Qualquer que seja o motivo da exclusão, premeditada ou não, é necessário saber quem a fez, pois há casos onde os arquivos deletados são dados/informações estratégicas para a organização e precisamos reportar o *meliante*.


Para contornar essa situação, vamos ativar a auditoria e avisar aos usuários sobre. Com certeza, todos irão ter mais atenção em suas ações. A seguir breve tutorial de como ativar este recurso, realizado no ***Windows Server 2019***:

## Configuração

No servidor, clique com o botão direito e logo após em ***Propriedades*** na ***Partição*** ou ***Pasta Compartilhada*** que deseja ativar a auditoria;
![Img 01](https://res.cloudinary.com/k4bv734/image/upload/v1637853863/blog_content/fileserver_1_aej9b7.png)
![Img 02](https://res.cloudinary.com/k4bv734/image/upload/v1637853863/blog_content/fileserver_2_y5vz4i.png)

Vá a aba ***Segurança*** e depois em ***Avançadas***;
![Img 03](https://res.cloudinary.com/k4bv734/image/upload/v1637853863/blog_content/fileserver_3_zwj1vv.png)

Na janela que se abre, clique na aba ***Auditoria***. Dependendo das suas configurações de segurança do usuário utilizado, será necessário clicar em ***Continuar***;


Clique em ***Adicionar*** na sequência;
![Img 04](https://res.cloudinary.com/k4bv734/image/upload/v1637853863/blog_content/fileserver_4_sprmn7.png)
![Img 05](https://res.cloudinary.com/k4bv734/image/upload/v1637853863/blog_content/fileserver_5_fshnzw.png)


Na próxima janela selecione o usuário ou grupo que deseja auditar;	
![Img 06](https://res.cloudinary.com/k4bv734/image/upload/v1637853864/blog_content/fileserver_6_hkfwnc.jpg)
	
Após selecionado, as opções ficarão disponíveis para edição. Clique em  ***Exibir permissões avançadas***. Provavelmente o usuário ou grupo selecionado já terá algumas permissões pré-definidas, desmarque todas e marque as opções ***Excluir subpastas e arquivos*** e ***Excluir***;


Em ***Tipo*** existem as opções ***Êxito***, ***Falha*** e ***Tudo***.
* ***Êxito***: para auditar apenas eventos de exclusão de arquivos concluídas com êxito
* ***Falha***: para auditar apenas eventos de exclusão de arquivos que falharam
* ***Tudo***: para auditar todos eventos de exclusão, concluídos e com falha


Clique em ***Ok*** em todas as janelas abertas;


Pronto, em partes... Acima somente configuramos a unidade/pasta onde desejamos que a auditoria funcione. Nos próximos passos iremos ativar a auditoria em si;


Presumo que você tenha um servidor de contas (Active Directory), neste execute ***gpedit.msc***;

Vá até ***Configurações do Computador > Configurações do Windows > Configurações de Segurança > Políticas Locais > Política de Auditoria***;

Abra a opção ***Auditoria de acesso a objetos***;
![Img 07](https://res.cloudinary.com/k4bv734/image/upload/v1637853864/blog_content/fileserver_7_mkpjzk.png)

Marque a opção ***Êxito*** para registrar apenas os registros dos arquivos excluídos. Caso seja seu desejo também registrar as tentativas de exclusão que falharam por motivo das configurações de restrições de acesso marque também a opção ***Falha***;
![Img 08](https://res.cloudinary.com/k4bv734/image/upload/v1637853863/blog_content/fileserver_8_uggopx.png)

Clique em ***Ok*** para aplicar as configurações e feche as janelas abertas;


Pronto, finalmente!


Agora é possível auditar os arquivos deletados. Para tal tarefa, acesse o ***Visualizador de Eventos*** em ***Ferramentas Administrativas*** ou pelo comando ***eventvwr***;


Navegue até os ***Logs do Windows > Segurança***;


Aqui serão listadas todos os registros de segurança do servidor. Para facilitar a visualização, filtre pelo ID do eventos (geralmente ***4663***);
![Img 09](https://res.cloudinary.com/k4bv734/image/upload/v1637853864/blog_content/fileserver_9_j7ezsd.png)


Configurada a auditoria de arquivos excluídos via mapeamento de rede.