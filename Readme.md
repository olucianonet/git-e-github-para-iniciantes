# 6. Extras

## Criando o `.gitignore`

- Ignorar e não *trackear* certos arquivos.
- Criar um arquivo chamado `.gitignore`.
- Dentro do arquivo, especificar os tipos ou nomes de arquivos a serem ignorados pelo git.

```
Profile
*.json
*.xls

```

- Mais em:
	- [Doc](https://git-scm.com/docs/gitignore)
	- [Template](https://github.com/github/gitignore)

## Git stash é lindo

- Guarda modificações ainda não commitadas temporariamente.

```
$ git st
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file2

$ git stash
Saved working directory and index state WIP on master: 0d184db add file1
$ git log
commit 0d184db65a59d829eaa3421615bca8182a03ffab (HEAD -> master)
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ git st
On branch master
nothing to commit, working tree clean
$ git co -b iss1
Switched to a new branch 'iss1'
$ git stash apply
On branch iss1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file2

$ git st
On branch iss1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file2

$ git ci -m 'add file2'
[iss1 737c612] add file2
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file2
$ git log
commit 737c612f1b09b5a2026d754f33d4a3191a0ab533 (HEAD -> iss1)
Date:   Thu Jan 23 19:03:14 2020 -0300

    add file2

commit 0d184db65a59d829eaa3421615bca8182a03ffab (master)
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ git co master 
Switched to branch 'master'
$ git stash clear
$ git stash list
$ git log
commit 0d184db65a59d829eaa3421615bca8182a03ffab (HEAD -> master)
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ git merge iss1 
Updating 0d184db..737c612
Fast-forward
 file2 | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file2
$ git log
commit 737c612f1b09b5a2026d754f33d4a3191a0ab533 (HEAD -> master, iss1)
Date:   Thu Jan 23 19:03:14 2020 -0300

    add file2

commit 0d184db65a59d829eaa3421615bca8182a03ffab
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ 
```

- Lista tudo o que estiver no stash. 

```
$ git stash list
```

- Limpa tudo o que estiver no stash. 

```
$ git stash clear
```

## Alias para que te quero

- Assim como no unix, é possível criar aliases para os comandos do git.
- Alguns aliases utilizados:

```
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg log --pretty=format:"%h %ad - %s" --date=short

```

## Versionamento com tags

- Utilizado para delimitar um grupo de commits.
- Criando uma tag:

```
$ git tag -a 1.0.0 -m 'Update file1'
```

- Enviando a tag para o Github

```
$ git push origin master --tags
```

- Listando as tags:

```
$ git tag
```

No Github, será criado um pacote com o source compactado e com a tag definida no formato de release.


## Salvando sua sexta com git revert

- Utilizado para voltar no fluxo de commits, mas não perder o histórico de alterações.
- Adicionando um novo arquivo e incluindo no versionamento com commit.

```
$ touch file3
$ git st
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	file3

nothing added to commit but untracked files present (use "git add" to track)
$ git add file3 
$ git st
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file3

$ git ci -m 'add file3'
[master 77dbe03] add file3
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file3
$ git st
On branch master
nothing to commit, working tree clean
$ git lg
77dbe03 2020-01-23 - add file3
737c612 2020-01-23 - add file2
0d184db 2020-01-23 - add file1
```

- Executando o revert do último commit

```
$ git revert 77dbe03
[master f1a5762] Revert "add file3"
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 file3
$ git lg
f1a5762 2020-01-23 - Revert "add file3"
77dbe03 2020-01-23 - add file3
737c612 2020-01-23 - add file2
0d184db 2020-01-23 - add file1
```

- Apesar do arquivo adicionado não existir mais no diretório, o commit continua no histório.

```
$ git st
On branch master
nothing to commit, working tree clean
$ git diff
$ ll
total 12
drwxr-xr-x 3 luciano luciano 4096 Jan 23 19:34 ./
drwxr-xr-x 5 luciano luciano 4096 Jan 23 18:57 ../
-rw-r--r-- 1 luciano luciano    0 Jan 23 18:58 file1
-rw-r--r-- 1 luciano luciano    0 Jan 23 19:03 file2
drwxr-xr-x 8 luciano luciano 4096 Jan 23 19:35 .git/
```

## Apagando tags e branches remotos

- Apagando tag localmente

```
$ git tag -d 1.0.0 
```

- Apagando tag remotamente

```
$ git push origin :1.0.0 
```

- Apagando branch localmente

```
$ git br -d nome-da-branch
```

- Apagando branch localmente

```
$ git push origin :nome-da-branch
```
