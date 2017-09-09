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



