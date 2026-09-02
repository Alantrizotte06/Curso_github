O git é utilizado para o versionamento do código e também no fluxo de desenvolvimento.

```jsx
git init //utilizado para iniciar um repositório
```

```jsx
git status //utilizado para passar o status da branch
```

**Branch:** É uma linha independente de desenvolvimento onde fica salvo o código sem afetar o código principal (main ou master).

Fluxo git:  

Diretório Local
↓
git add
↓
Área de preparação (staging) 
↓
git commit
↓
Repositório Local
↓
git push
↓
Repositório Remoto

## Consultando registros

```jsx
git log //serve para acessar os registros de commits
```

!image.png

## Criando Branch

```jsx
git branch //lista todas as branchs.
git branch exemplo //criando uma nova branch.
git checkout exemplo //estou saindo da branch main e indo para a branch exemplo.
```

Outro atalho caso a branch ainda não esteja criada é:

```jsx
git checkout -b corrige-bug //estamos criando uma nova branch e entrando nela
```

Agora para integrar o histórico que está na branch “exemplo” para a branch main, segue o comando:

```jsx
git merge exemplo //Este comando é utilizado para integrar o histórico da branch "exemplo" na main
```

## Conflitos na branch

O Git encontra alterações incompatíveis que não consegue combinar automaticamente, para resolver manualmente é necessário realizar o git merge e aceitar a alteração atual e depois inserir o que há de novo manualmente, assim é feito a correção manual de conflitos.

---

August 10, 2026 

## Rebase

O rebase é utilizado para manter a ordem cronológica de commits linear, porem pesquisei e dentro de um ambiente de trabalho o rebase é mais utilizado para fazer atualizações na sua branch local e se manter atualizado.

```jsx
git switch exemplo //comando utilizado para mudar a branch em que estamos.
```

## Rebase na Pratica (Trabalho)

Rebase: É utilizado para reorganizar/replicar os commits de uma branch para uma nova base, mantendo o histórico mais linear e atualizando uma branch com alterações mais recentes.

Merge: É utilizado para integração de branches.

## Aprendendo git utils

### Git stash

O git stash é utilizado para quando quero salvar temporariamente um código sem precisar criar um commit, exemplo: o código ainda não está completo ou vou trabalhar em outra branch, e etc…

```jsx
git stash exemplo
git stash list //Lista todos os arquivos salvos temporariamente.
git stash apply exemplo //Acessa o arquivo que foi salvo.
git restore --staged Login.ts //Remove o arquivo da staging area, mantendo as alterações no diretório de trabalho.
```

---

August 11, 2026 

## Logs

Para acessar algum commit anterior é necessário executar o seguinte comando:

```jsx
git checkout (aqui vai a hash do commit)
git log exemplo //Vai trazer todos os logs da branch exemplo.
git log --pretty=oneline //Vai trazer os logs mais descritivos em uma linha.
git log --pretty=format:"%h - %an - %ar - %s" //Vai trazer informações do commit em data, nome autor e etc...
```

Buscando commits por datas:

```jsx
git log --since="1 day ago" //Vai trazer todos os commits feitos há um dia atras.
```

Filtros de texto nos commits:

```jsx
git log --grep="teste" //Vai trazer todos os commits escrito teste
```

Verificando o log de merge:

```jsx
git log --merges //Mostra commits de merge no histórico.
```

Filtro de logs de duas branchs apenas:

```jsx
git log master...exemplo //Traz apenas os apenas os commits das duas branchs.
```

## Gitignore

O git ignore define arquivos e diretórios que o Git deve ignorar e, portanto, normalmente não serão adicionados ao controle de versão.

!image.png

---

August 15, 2026 

## Criando aliases no git

Este recurso é utilizado para salvar um comando e executar com uma palavra chave, exemplo de um comando muito longo para gerar o gráfico de logs no git.

 

```jsx
git config --global alias.hc "log --graph --oneline --decorate --all" //Este comando está sendo executado para quando eu digitar hc ele execute o comando entre aspas.
```

## Hooks

São scripts automatizados que são disparados quando algum evento ocorre no ciclo de vida do Git, podemos utiliza-los em em automatização de tarefas de qualidade do código, testes e integração continua, para garantir que não suba nenhum código quebrado ou fora do padrão para o repositório. Segue exemplo de acesso aos hooks predefinidos:

!image.png

```jsx
chmod +x .git/hooks/pre-commit //Exemplo de como permitir a execução do arquivo.
```

```jsx
#!/bin/bash

echo "é necessário uma ação" //Exemplo de como escrever o arquivo pre-commit
```

## Padrões de commit com Hook

Podemos definir um padrão de como devem ser os commits, por exemplo todos commit deve iniciar com feat, fix, refactor ou chore, para isso realizamos a configuração dentro do arquivo commit-msg.

!image.png

```jsx
#!/bin/bash

COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat "$COMMIT_MSG_FILE")

if ! echo "$COMMIT_MSG" | grep -qE "^(feat|fix|chore|refactor):"; then
        echo "Erro: A mensagem do commit deve começar com 'feat:', 'fix:', 'refactor:'  ou 'chore:'."
        exit 1
fi //Validação se o commit inicia com os critérios.
if [ ${#COMMIT_MSG} -gt 72 ]; then
        echo "Erro: A mensagem de commit deve ter no máximo 72 caracteres."
        exit 1
fi//Validação se o commit possui até 72 caracteres.

echo "Tudo certo, parabéns!" 
```

### Alterar nome de arquivo

```jsx
mv .git/hooks/commit-mgs .git/hooks/commit-msg //Realizando a alteração do nome do arquivo.
```

---

August 18, 2026 

## Configurando o repositório no git

Esta aula em especifico foi ensinando a criar o repositório remoto no git, com comando como git remote e git push, por boa prática é melhor utilizar o nome main ao invés da master.

```jsx
git remote //Lista o repositório remoto do projeto.
git remote add //Comando executado para direcionar o repositório remoto do projeto.
git push origin main //Envia os commits da branch main local para a branch main do repositório remoto origin.
git remote remove //Utilizado para remover o repositório remoto.
```

---

August 23, 2026 

## Pull Request

O pull request (PR) é utilizado para quando queremos enviar alterações de alguma branch para a branch **main**

## Git fetch

É utilizado para trazer as alterações do repositório remoto.

---

September 1, 2026 

## Histórico de Log e Alterações

Para verificar as alteração de todos os commits de um arquivo especifico é necessário realizar o seguinte comando:

```jsx
git log -p -- themes/exemplo.html //Comando para verificar alterações e commits, o -- serve como boa prática para evitar ambiguidades entre nome de branch e arquivos.
git blame -p -- themes/exemplo.html //Comando para exibir detalhamento de quem realizou a alteração, commit e quais linhas foram alteradas

```

## Git cherry-pick

Serve para copiar um commit específico de qualquer branch e aplicá-lo na sua branch atual. Segue o comando:

```jsx
git cherry-pick (hash do commit) //Este comando vai cópiar as alterações de um commit especifico da branch exemplo para a atual, deve ser inserido o hash do commit. 
```