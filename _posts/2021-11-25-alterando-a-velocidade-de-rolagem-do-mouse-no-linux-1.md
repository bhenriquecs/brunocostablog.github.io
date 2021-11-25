---
date: 2020-12-17 00:00:00
layout: post
title: Alterando a velocidade de rolagem do mouse no Linux
description: Um "problema" que tive no Linux, na distro Ubuntu, era na
  velocidade do botão de rolagem do mouse.
category: blog
author: brunocosta
paginate: false
---
Um "problema" que tive no Linux, na distro Ubuntu (para aqueles que estão iniciando em Linux, este é baseado no Debian), era na velocidade do botão de rolagem do mouse. Por padrão tive muita lentidão nas rolagem de páginas.
Para resolver, utilizei o Inwheel. Aqui estarei utilizando como base o Ubuntu 20.04.

	1. Instale o Imwheel
		a. Abra o Terminal (Crtl + Alt + T)
		b. Dê o comando e digite sua senha root (administrador)
		sudo apt-get install imwheel
		
	2. Configuração
		a. Baixe ou crie um novo documento Bash (.sh) com o script existente neste link http://www.nicknorton.net/mousewheel.sh (Obrigado!)
		b. Se você for iniciante no mundo Linux, pode encontrar alguma dificuldade na tarefa acima. Um exemplo de como poderá ser feito de forma simples e utilizando o ambiente gráfico:
			i. Clique no link que contém o script
			ii. Copie o código
			iii. Abra o menu de aplicativos e execute o "Editor de texto"
			
			iv. No Editor de texto cole o código copiado anteriormente
			v. Clique em "Salvar", escolha um diretório e salve com o nome "mousewheel.sh"
			
		c. Agora vamos executar o arquivo no Terminal
			i. Será necessário acessar o Terminal e ir até o diretório onde salvou o script Bash. Uma forma simples de fazê-lo é acessando a pasta onde encontra-se o arquivo, clicar com o botão direito do mouse em uma área vazia da pasta e ir em "Abrir no Terminal"
			
		d. No Terminal, primeiro vamos dar permissão de execução usando o comando
		chmod +x mousewheel.sh
		
		e. Agora vamos executar o script
		sudo ./mousewheel.sh
		
		f. Será solicitada a senha root, digite-a e dê enter
		g. Se tudo correr bem, será apresentada a tela onde conseguirá definir a velocidade da rolagem do mouse. Indico definir em 3, porém fica a seu critério. Por fim clique em "Apply"
		
		h. Pronto! Faça o teste e veja que a rolagem está bem mais ágil
		i. Caso queira aumentar ou diminuir a rolagem, basta executar o script novamente
		j. Para aqueles que possuem mouse com botões extras além dos dois padrões e rolagem, caso encontrem algum problema nestes adicionais, tente adicionar -b "4 5" ao Imwheel. No terminal dê o comando:
		imwheel -b "4 5"
	
	3. Configurando o Imwheel para iniciar na reinicialização
		Por padrão o Imwheel não irá carregar a configuração realizada a cada reinicio do sistema, tendo assim que fazer todo o procedimento novamente. Embora seja uma tarefa simples, é um trabalho adicional que precisamos contornar, haha. Faça o seguinte:
		a. No Menu de aplicativos pesquise por "aplicativos iniciais", caso utilize o sistema em inglês "startup applications"
		
		b. Na próxima janela, clique em "Adicionar"
		c. Digite:
			i. Nome = Imwheel
			ii. Comando = selecione o arquivo .sh (mousewheel.sh)
			iii. Comentário = Escreva o que quiser
		
		d. Clique em "Adicionar" e terá terminado as configurações!
		
	4. Manual
	Para obter mais detalhes do Imwheel, digite no Terminal para acesso ao manual
	man imwheel
	
Fonte:
https://dev.to/bbavouzet/ubuntu-20-04-mouse-scroll-wheel-speed-536o
https://io.bikegremlin.com/11541/linux-mouse-scroll-speed/

