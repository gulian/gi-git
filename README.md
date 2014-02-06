Explications du SCM Git
=====================================

## initialisation

### Le dépôt n'existe pas : `git init` 

### Le dépôt existe : `git clone` 
```
> git clone http://github.com/gulian/gi-git
ou
> git clone https://github.com/gulian/gi-git
ou
> git clone git://github.com/gulian/gi-git.git
```

Sortie de la commande : 
```
Cloning into 'gi-git'...
remote: Counting objects: 12, done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 12 (delta 3), reused 6 (delta 1)
Unpacking objects: 100% (12/12), done.
```
Vous avez maintenant une copie local du dépôt distant, et un working tree propre. Vérification avec la commande : `git status` :

```
# On branch master
nothing to commit (working directory clean)
```

(N'oubliez pas de rentrer dans le dépôt `cd gi-git`)

## Opération de base 

### Commit, travail sur le working tree

#### Modification ou création d'un fichier (`echo 'pwd' >> pwd.txt`)

```
> git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	pwd.txt
nothing added to commit but untracked files present (use "git add" to track)
```

Le fichier n'est pas actuellement présent sur le dépôt. Pour l'ajouter au `working tree` : `git add`
```
> git add pwd.txt
ou 
> git add . 
ou 
> git add *.txt
```

Vérification avec la commande : `git status` :
```
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	new file:   pwd.txt
#
```
