# Várias configurações de chaves SSH para diferentes contas do github

## criar uma chave pública diferente

crie uma chave ssh diferente para ada conta do github

```
ssh-keygen -t rsa -C "alexcesar.n@gmail.com"
```

```
ssh-keygen -t rsa -C "acn.negociosdigitais@gmail.com"
```



por exemplo, 2 chaves criadas em:

```
~/.ssh/id_rsa_git1
~/.ssh/id_rsa_git2
```

em seguida, adicione essas duas chaves da seguinte maneira

```
eval `ssh-agent -s`
ssh-add ~/.ssh/id_rsa_git1
```
```
eval `ssh-agent -s`
ssh-add ~/.ssh/id_rsa_git2
```

você pode excluir todas as chaves em cache antes

```
ssh-add -D
```

finalmente, você pode verificar suas chaves salvas

```
ssh-add -l
```

## Modifique a configuração ssh

```
$ cd ~/.ssh/
$ touch config

```

Entre no arquivo config e configure conforme exemplo abaixo:

```
#git1 account
Host github.com-alexcesarnascimento
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_git1

#git2 account
Host github.com-acn
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_git2
```

## Clone seu repositório e modifique o Git Config

clone seu repositório: E modifique o usuario

```
git config --add user.name "AlexCesarNascimento"
git config --add user.email "alexcesar.n@gmail.com"
```

```
git config --add user.name "StartACN"
git config --add user.email "acn.negociosdigitais@gmail.com"
```



O Git vem com uma ferramenta chamada `git config` que permite configurar variáveis que controlam todos os aspectos de como o git irá operar

`git config` mantém seu valor entre as atualizações. Então, você precisa configurá-lo apenas uma vez.

Basicamente, existem 3 lugares para armazenar essas variáveis:

1. Sistema.

2. Global.

3. Local.


------
**Sistema:** Estas variáveis estão disponíveis para cada usuário no sistema e armazenadas em

`[path]/etc/gitconfig`.
**Exemplo:** `C:/Program Files/Git/etc/gitconfig`

------

**Global**: As configurações globais estão disponíveis para os usuários atuais para todos os projetos e armazenadas em

`~/.gitconfig` ou `~/.config/git/config`
**Exemplo:** `C:/Users/Username/.gitconfig`

Você pode fazer o git ler e escrever no Global passando a opção --global.

------

**Local**: As configurações locais estão disponíveis apenas para o repositório atual. Você pode fazer o git ler e escrever no Local passando a opção --local.

Além disso, é importante lembrar que cada nível substitui os valores do nível anterior.

------

**Prioridade:** Local > Global > Sistema

```
Create a local specific config
$ git config --local user.name "Local User"

# Create a global config
$ git config --global user.name "Global User"

# Create a system config
$ sudo git config --system user.name "System User"
```

para verificar a origem da sua configuração:

```
git config --list --show-origin
```

