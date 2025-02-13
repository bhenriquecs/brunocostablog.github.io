---
date: 2025-02-12 20:58:07
layout: post
title: Repositório no GitHub e deploy automático via FTP
description: Essa automação é útil para desenvolvedores e empresas que utilizam
  VPS e/ou hospedagens compartilhadas para hospedar seus projetos. É ideal para
  quem quer automatizar o processo de deploy, evitando o envio manual de
  arquivos via FTP, garantindo rapidez, consistência e menos erros no lançamento
  de atualizações.
image: https://res.cloudinary.com/k4bv734/image/upload/v1739403114/blog/github-deploy-ftp_au6kal.png
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1739403113/blog/github-deploy-ftp_optimized_adr00z.png
category: desenvolvimento
tags:
  - github
  - ftp
author: brunocosta
paginate: false
---
Se você deseja automatizar o envio do seu código para uma hospedagem via FTP utilizando GitHub Actions, este guia vai te ajudar a configurar um workflow que fará o deploy automaticamente sempre que houver uma nova alteração no repositório.

Essa automação é útil para desenvolvedores e empresas que utilizam VPS e/ou hospedagens compartilhadas para hospedar seus projetos. É ideal para quem quer automatizar o processo de deploy, evitando o envio manual de arquivos via FTP, garantindo rapidez, consistência e menos erros no lançamento de atualizações.

### Passo 1: Criando o Repositório e Configurando o Ambiente

Antes de configurar o deploy automático, siga estas etapas:

**Instale as ferramentas necessárias:** 

* [Git](https://git-scm.com/)
* [GitHub Desktop](https://desktop.github.com/)
* [Visual Studio Code](https://code.visualstudio.com/)

**Crie um repositório local** 

No terminal, navegue até a pasta do projeto e execute:

```
git init
```

**Crie um repositório no GitHub e sincronize-o** 

Na sua conta do GitHub, crie um novo repositório.

No GitHub Desktop, clone ou conecte o repositório local e publique no GitHub.

 **Crie a pasta de workflows para automação** 

No terminal, execute:

```
mkdir-p .github/workflows
```

### Passo 2: Criando o Arquivo de Workflow

Agora, dentro da pasta `.github/workflows`, crie um arquivo chamado `ftp-deploy.yml` e adicione o seguinte código YAML:

```
name: Deploy to FTP
 
# Define quando o workflow será executado
on:
  push:
    branches:
      - main # Altere para o branch que você utiliza
        workflow_dispatch: # Permite execução manual

jobs:
  ftp-deploy:
    runs-on: ubuntu-latest
    steps:
      # Faz o checkout do código no repositório
      - name: Checkout do repositório
      uses: actions/checkout@v3
			
      # Usa a ação FTP Deploy para enviar arquivos ao servidor
      - name: Deploy para FTP
        uses: SamKirkland/FTP-Deploy-Action@v4.3.5

      with:
        server: 127.0.0.7 # Substitua pelo endereço do seu FTP
        username: ${{ secrets.FTP_USERNAME }} # Variável de ambiente para o nome de usuário
        password: ${{ secrets.FTP_PASSWORD }} # Variável de ambiente para a senha
        local-dir: ./ # Diretório local (raiz do repositório)
        server-dir: /path # Caminho no servidor FTP
```

### Passo 3: Configurando os Secrets no GitHub ###

Para garantir a segurança das credenciais do FTP, utilizamos *Secrets* do GitHub. Siga os passos para configurá-los:


**1.** Acesse o repositório no GitHub.


**2.** Vá até Settings > Secrets and variables > Actions > New repository secret.


**3.** Adicione os seguintes secrets:


**FTP_USERNAME:** Seu nome de usuário FTP.

**FTP_PASSWORD:** Sua senha FTP.

### Passo 4: Testando o Workflow ###


Após configurar tudo, faça um commit e push no repositório para testar a automação. Utilize o Visual Studio + o Github Desktop ou o exemplo abaixo usando o terminal:
```


git add .
git commit -m "Configuração de deploy automático via FTP"
git push origin main
```



Agora, acesse a aba *Actions* no GitHub e verifique se o workflow foi executado corretamente.



Com este processo, você terá um sistema automatizado que fará o deploy do seu projeto sempre que houver alterações no branch principal (ou no branch que informou no arquivo de workflow). Isso melhora a eficiência do desenvolvimento e reduz a necessidade de uploads manuais via FTP.