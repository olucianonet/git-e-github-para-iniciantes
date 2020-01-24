# 04. Ramificação (Branch)

## O que é um branch e por que usar?

>*"É um ponteiro que leva a um commit."*

- Preserva o `master`
- Trabalho simultâneo
- Evita conflitos

## Criando um branch

- Criando um novo branch de nome testing.

```
$ git co -b testing
Switched to a new branch 'testing'
```

É criando um novo branch, que dará origem a uma ramificação do master

- Listar os branches existentes, identificando o atual.

```
$ git br
 master
* testing
```

- Criando um novo branch vazio.

```
$ git co --orphan empty-branch
Switched to a new branch 'empty-branch'
```

É criado um novo branch, porém com os arquivos somente no stage, sem commits.

```
$ git show
fatal: your current branch 'empty-branch' does not have any commits yet
$ git st
On branch empty-branch

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   new-file.md
	new file:   Readme.md
```

Remova os arquivos no stage e o branch estará completamente vazio.

```
$ git rm -rf .
rm 'new-file.md'
rm 'Readme.md'
$ git st
On branch empty-branch

No commits yet

nothing to commit (create/copy files and use "git add" to track)

```

## Movendo e deletando branches

- Para listar e alterar entre os branches, utilize:

```
$ git br
* master
  testing
$ git co nome-do-branch
```

- Deletando um branch

```
$ git br -D new-branch 
Deleted branch new-branch (was d0985c5).
```

**Importante:** Antes de sair de um branch, realize o commit de todas as alterações.

## Entendendo o merge

- Mantém o histórico dos commits anteriores em todos os branches.
- Cria um commit somente para fazer a união dos branches, pode afetar a legibilidade da árvore.

## Entendendo o rebase

- Insere o novo ramo na frente do último commit da master.
- Altera o histórico, prejudicando a ordem cronológica.
- Exemplo:

```
$ git pull --rebase
```

## Merge e rebase na prática

- merge: utilizado mais em pull request, para demonstrar a união de dois branches.

```
*   4f3bc99 (HEAD -> master) Merge branch 'iss1'
|\  
| * 0d10cb7 (iss1) Add file3
* | d0e0074 Add file4
|/  
* d1cf62b Add file2
* 2203974 add file1
```

- rebase: 

```
* cfb12d7 (HEAD -> master) Add file4
* 9589576 (iss1) Add file3
* a25161a Add file2
* d66e61d Add file1
```
