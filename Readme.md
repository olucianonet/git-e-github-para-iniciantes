# 03. Repositórios Remotos

## Criando um repositório no Github

- Com uma conta ativa no Github, 

<!-- ![Github](images/github-home.png) -->

- crie e configure um novo repositório.

<!-- ![Github](images/create-new-repo.png) -->

## Criando adicionando uma chave SSH

- Gerar uma nova chave ssh (*Debian 10*)

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- Será solicitado um nome para o arquivo id_rsa e uma passphrase:

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

- Adicione a chave ssh ao ssh-agent

```
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

- Adicione a chave ssh ao Github

Copie sua chave pública e crie um novo registro de chave nas configurações do Github

<!-- ![](images/add-new-ssh-key.png)  -->

## Ligando repositório local a um remoto

- Utilize as instruções exibidas no momento da criação do repositório:

```
…or create a new repository on the command line

echo "# git-e-github-para-iniciantes" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:olucianonet/git-e-github-para-iniciantes.git
git push -u origin master

…or push an existing repository from the command line

git remote add origin git@github.com:olucianonet/git-e-github-para-iniciantes.git
git push -u origin master
```

## Enviando mudanças para um repositório remoto

- Após enviar pro stage e realizar o commit das alterações:

```
$ git push origin master
```

- Realizando o push de todos os branches.

```
$ git push --all origin
```

## Clonando repositórios remotos

- Prefira ssh por ser mais rápido.

```
$ git clone gitgit@github.com:olucianonet/git-e-github-para-iniciantes.git
```

## Fazendo fork de um projeto

- Copia um projeto de terceiros.

	- Realizar um fork do projeto para sua conta do Github
	- Realizar as alterações
	- Enviar um pull-request para as alterações serem adicionadas ao projeto original.
