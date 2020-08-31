---
layout: post
title:  "Git - Comandos Básicos"
date:   2020-08-30 17:09:00
categories: Git; Comandos
---

# Git - Comandos básicos

Trata-se de mera compilação de comandos básicos para o manejo diário do Git.



## 1. Criar um novo repositório

Primeiramente, para melhor organização dos arquivos e pastas, acredito que seja melhor criar uma nova pasta. 

Após isso, podemos abrir o terminal e digitar o comando:
`git init`

Assim, será criado um novo repositório.



## 1.1 Clonando um repositório já existente

1. Caso seja necessário importar um repositório já existente, podemos cloná-lo em um repositório local, para isso, digitamos o comando
   `git clone /caminho/para/o/repositório`

2. Caso o repositório esteja contido em um servidor remoto, devemos digitar o seguinte comando
   `git clone usuário@servidor:/caminho/para/o/repositório`



## 2. Adicionar - Comando add

Você pode propor mudanças  usando
`git add <arquivo>`

Ou, para dicionar todos os arquivos modificados, usa-se o comando:
`git add *` 



## 3. Confirmar as alterações - Comando commit

Este é o primeiro passo no fluxo de trabalho básico do git. Para realmente confirmar estas mudanças (isto é, fazer um *commit*), use
`git commit -m "comentários das alterações"`
Agora o arquivo é enviado para o **HEAD**, mas ainda não para o repositório remoto.



## enviando alterações

Suas alterações agora estão no **HEAD** da sua cópia de trabalho local. Para enviar estas alterações ao seu repositório remoto, execute
`git push origin master`
Altere *master* para qualquer ramo (*branch*) desejado, enviando suas alterações para ele.

Se você não clonou um repositório existente e quer conectar seu repositório a um servidor remoto, você deve adicioná-lo com
`git remote add origin <servidor>`
Agora você é capaz de enviar suas alterações para o servidor remoto selecionado.



## ramificando

*Branches* ("ramos") são utilizados para desenvolver funcionalidades isoladas umas das outras. O branch *master* é o branch "padrão" quando você cria um repositório. Use outros branches para desenvolver e mescle-os (*merge*) ao branch master após a conclusão.

![img](http://rogerdudler.github.io/git-guide/img/branches.png)

crie um novo branch chamado "funcionalidade_x" e selecione-o usando
`git checkout -b funcionalidade_x`
retorne para o master usando
`git checkout master`
e remova o branch da seguinte forma
`git branch -d funcionalidade_x`
um branch *não está disponível a outros* a menos que você envie o branch para seu repositório remoto
`git push origin <funcionalidade_x>`



## atualizar & mesclar

para atualizar seu repositório local com a mais nova versão, execute
`git pull`
na sua pasta de trabalho para *obter* e *fazer merge* (mesclar) alterações remotas.
para fazer merge de um outro branch ao seu branch ativo (ex. master), use
`git merge <branch>`
em ambos os casos o git tenta fazer o merge das alterações automaticamente. Infelizmente, isto nem sempre é possível e resulta em *conflitos*. Você é responsável por fazer o merge estes *conflitos* manualmente editando os arquivos exibidos pelo git. Depois de alterar, você precisa marcá-los como merged com
`git add <arquivo>`
antes de fazer o merge das alterações, você pode também pré-visualizá-as usando
`git diff <branch origem> <branch destino>`



## rotulando

é recomendado criar rótulos para releases de software. Este é um conhecido conceito, que também existe no SVN. Você pode criar um novo rótulo chamado *1.0.0* executando o comando
`git tag 1.0.0 1b2e1d63ff`
o *1b2e1d63ff* representa os 10 primeiros caracteres do id de commit que você quer referenciar com seu rótulo. Você pode obter o id de commit com
`git log`
você pode também usar menos caracteres do id de commit, ele somente precisa ser único.



## sobrescrever alterações locais

No caso de você ter feito algo errado (que seguramente nunca acontece ;) ) você pode sobrescrever as alterações locais usando o commando
`git checkout -- <arquivo>`
isto substitui as alterações na sua árvore de trabalho com o conteúdo mais recente no HEAD. Alterações já adicionadas ao index, bem como novos arquivos serão mantidos.

Se ao invés disso você deseja remover todas as alterações e commits locais, recupere o histórico mais recente do servidor e aponte para seu branch master local desta forma
`git fetch origin`
`git reset --hard origin/master`



## Links úteis

Site Oficial do GIT: https://git-scm.com/

Manual Oficial do GIT: https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Sobre-Controle-de-Vers%C3%A3o