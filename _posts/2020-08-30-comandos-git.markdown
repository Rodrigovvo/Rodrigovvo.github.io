---
layout: post
title:  "Git - Comandos Básicos"
date:   2020-08-30 17:09:00
categories: Git; Comandos
---



Trata-se de mera compilação de comandos básicos para o manejo diário do Git, de uso pessoal para minhas consultas rápidas.



## 1. Criar um novo repositório

Primeiramente, para melhor organização dos arquivos e pastas, acredito que seja melhor criar uma nova pasta. 

Após isso, podemos abrir o terminal e digitar o comando:
`git init`

Assim, será criado um novo repositório.



### 1.1. Clonando um repositório já existente

1. Caso seja necessário importar um repositório já existente, podemos cloná-lo em um repositório local, para isso, digitamos o comando
   `git clone /caminho/para/o/repositório`

2. Caso o repositório esteja contido em um servidor remoto, devemos digitar o seguinte comando
   `git clone usuário@servidor:/caminho/para/o/repositório`



## 2. Adicionar - Comando add

As alterações que você fizer nos documentos constantes no repositório, devem ser adicionadas utilizando-se o comando:
`git add <nome_do_arquivo>`

Ou, para adicionar todos os arquivos modificados, usa-se o comando:
`git add *`
ou
`git add . `



## 3. Confirmar as alterações - Comando commit

Confirmada a alteração, devemos fazer um *commit* das alterações, usando o seguinte comando
`git commit -m "explicação da alteração"`

Através desse comando o arquivo é enviado para o branch atual, que também é chamada de (*Head*).



## 4. Enviar alterações para o Repo. - Comando push

Considerando que as informações e alterações estão na branch selecionada, devemos enviar os arquivos alterados para o repositório remoto, devendo executar o comando: 
`git push origin master`



## 5. Ramificações - Branch

Crie um novo branch usando o comando :
`git checkout -b <nome_da_branch>`

Após a criação, envie a branch para o repositório remoto  para que fique disponível para a nível do respositorio remoto para os outros, usando o seguinte comando:
`git push origin <nome_da_branch>`

Navegue entre as branches  existentes usando o comando:
`git checkout <nome_da_brach>`

Exclua uma branch, usando o seguinte comando:
`git branch -d <nome_da_branch>`

## 6. Atualizar - Comando pull

Para atualizar o repositório local com a versão mais recente do repositório remoto, utiliza-se o comando:
`git pull`



## 7. Utilizando Tags - Comando Tag

### 7.1. Id do commit - Comando Log

Você pode obter o id de commit utilizando o seguinte comando:
`git log`

Utilizo os primeiros caracteres do id de commit para criar a Tag

### 7.2. Criando a Tag

Pode-se criar uma Tag executando o seguinte comando:
`git tag <nom_da_tag> <primeiros_chars_do_id_do_Log>`

Por padrão uso os primeiros 10 números mas pode-se também usar menos caracteres do id, contudo é necessário garantir que seja uma chave única.



## 8. Sobrescrever alterações locais

Para sobrescrever as alterações locais usando, no caso de ter cometido algum erro, deve-se executar o commando:
`git checkout -- <arquivo>`

## Links úteis

Site Oficial do GIT: https://git-scm.com/

Manual Oficial do GIT: https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Sobre-Controle-de-Vers%C3%A3o