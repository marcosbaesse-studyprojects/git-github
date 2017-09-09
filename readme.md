# Curso Git e Github

## Configuração Inicial

### Nome
git config --global user.name "Nome Usuário"

### Email
git config --global user.email email@example.com

### Cores
git config --global color.ui true


## Os 3 estágios

### Como criar um repositório

Repositório é uma pasta configurada para o git realizar o controle de versão

Na pasta a ser controlada, deve inicializar o diretório
```$ git init ```

Ao se inicializar uma pasta, um direorio oculto é criado: .git

Para se remover o controle de versão de um diretório, basta excluir o diretório .git

Para se verificar o estágio de um diretório, basta executar:
``$ git status```

### Primeiro Estágio: Untracked Files

Untracked Files são arquivos que não estão sendo controlados pelo git.

### Segundo Estágio: Stagging (Changes to be commited)

Os arquivos entram nesse estágio quando são adicionados através do comando ```$ git add {arquivo.extensao}```

Este é o estágio em que os arquivos estão prontos para entrar no cotrole de versão, mas ainda não estão no controle de versão

### Terceiro Estágio: Arquivos commitados

São os arquivos que fazem parte do controle de versão. Os arquivos são adicionados neste status através do comando ```$ git commit -m "Comentário do Commit"```

Através do comando ```$ git log ``` é possível visualizar o histórico do controle de versão


## Realizando o primeiro commit

### Adicionando arquivos

O(s) parâmetro(s) do ```$ git add``` é útil para se especificar quais arquivos devem entrar no segundo estágio.
Em situações onde tenha de adicionar todos, o seguinte comando é indicado ```$ git add .```

Após o git add, há diversas formas de se realizar o commit, segue alguns exemplos:
* git commit -m 'descricao'
* git commit
* git commit -a

O primeiro método commit é indicado para situações em que há pouco a ser descrito acerca do commit.
Já o segundo método é muito bom para se 
descrever várias mudanças em um mesmo commit.

## Verificando Log

O Log (registro) de commits é visualizado através do comando ```$ git log ```

Ele possui diversas opções:
* -p: Mostra as diferenças (em código) entre os arquivos antes e depois do commit
* -p -2: Mostra as diferenças dos dois últimos commits
* --stat: Mostra estatísticas dos commits. Um resumo da quantidade de alterações nos arquivos
* --pretty-oneline: Mostra a formatação do commit em uma linha.
* --pretty-{outras-opções}: Existem muitas formatações disponíveis para o --pretty.
* --since=X.days: Mostra os commits desde X dias/semanas/meses

## Ignorando arquivos
Existem arquivos pessoais e que não são interessantes sendo controlados pelo CV do Git.
(arquivos com senhas pessoais, configurações de IDEs e Editores, ...)

Para que estes arquivos não entrem em controle de versão, basta adicioná-los a um arquivo '.gitignore' na raiz do projeto

## Brincando com fluxo de commits

* Para voltar um arquivo no estágio 2: ```$ git reset HEAD <file>```

## Voltando versões

A forma mais simples é com o git checkout
O git checkout é dado com o hash que identifica um commit.

Outra forma é o git reset HEAD~N
Onde N é o número de commits que se deseja voltar

Outra forma com o reset HEAD é git reset HEAD~1 --soft
remove o arquivo apenas do controle do git, mas mantém suas modificações

Já o git reset HEAD~N --hard, além de remomer os arquivos do commit, ele ainda remove as alterações do arquivo.

## Falando sobre branches
 
O git trabalha com snapshots.
Ele usa a linha do tempo principal (master) para controlar as versões.

As branchs são linhas do tempo alternativas, utilizadas para o desenvolvimento de partes de um projeto que ainda não foram aprovadas para integrarem à obra principal. 

Essas branchs são integradas ao projeto principal através de um merge. Após integradas, normalmente, não existe necessidade de mantê-las. Visto que elas já fazem parte do projeto principal


## Criando o primeiro branch

O comando git checkout é utilizado para se criar branchs
O parâmetro -b indica que um novo branch deve ser criado

Se não passar parâmetro -b, significa que se está trocando de branch

O comando git branch mostra as branchs do repositório

Tudo que é criado em um branch não é visível pelos demais branchs. O demais branchs só podem visualizar tais mudanças quando realizam um merge com o branch necessário.

É interessante se criar branchs sempre que for implementar uma funcionalidade ou atender á uma ussue (tarefa/problema)


## Merge e Rebase

Merge é a ação de mesclar branchs

O comando para se mesclar branchs é git merge <branch>. Através dele, a branch atual é mesclada (recebe as mudanças) da branch informada

O merge gera um commit que registra aquele merge.
Como nem todas as branchs devem ser compartilhadas entre o time, este commit pode não ser relevante.

Para estes casos, é interessando utilizar o comando rebase

O rebase reorganiza os commits, mas não gera um novo commit quando faz o merge.


## Criando chave pública para Github

O github sempre pede autenticação quando se deseja enviar arquivos do repositório local para o repositório do github.

Para não ter de digitar a senha a cada 'push', deve configurar um chave pública e uma chave privada, que serão responsáveis por realizar uma autenticação mais prática e mais segura que a autenticação https

O comando para gerar a chave é ssh-keygen

Para saber se a chave foi gerada, pode-se entrar no diretório .ssh da pasta home

Neste diretórios,  as chaves possuem o nome id_rsa (privada) e id_rsa.pub(pública)

No github, vai em account settings, e cadastra a chave pública do sistema


## Primeiro push

A tradução de push é 'empurrar'. No git, push tem o sentido de empurrar/enviar um repositório local para um repositório remoto.

Para que o git saiba qual o reposotório remote, deve-se utilizar o git remote

Um repositório local pode contrubuir para vários repositórios remotos. Mas o repositório padrão, normalmente e por convensão, é o origin. Os principais psuhes devem ser enviados ao origin.

O git remote é o comando para gerenciar os repositórios remotos.

Basicamente o comando é git push origin master

## Dando push em outro branch

No comando git push origin <branch> especifica a branch desejada a ser criada no servidor e que irá receber o push

## Fazendo clone

O clone serve para se baixar um repositório remoto para o computador local.

COm o git branch -a pode-se visualizar os branchs locais e remotos
Para criar um branch local que seja semelhante a um branch remoto se utiliza
git checkout -b <branch> origin/<branch>


## Push e Pull com novo branch

O comando push empurra atualizações para o servidor
O comando pull pega atualiações do servidor


## Criar um repositrório remoto em máquina local

Esse repositório é criado através do comando git init --bare

Este repositório é apenas um repositório de serviço, não de trabalho

os comando são executados da mesma forma que no github. A diferença é que assim, vc informa o enderço e a pasta do projeto

## Git hook

Um exemplo do git hook é para que os pushs sejam enviados ao site automaticamente

dentro do repositório bare, tem uma pasta hooks, com diversos enventos

Tem um arquivo chamado post-receive, que deve conter o seguinte código:

#!/bin/sh
GIT\_WORK\_TREE=/Users/wesley/gitCode/meusite.com.br git checkout -f

