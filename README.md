Explications git
================

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

Il ne reste plus qu'à commité les modifications sur le `local tree` :

```
> git commit -m "Ajout d'un fichier de texte contenant le répertoire courant"
[master 6463759] Ajout d'un fichier de texte contenant le répertoire courant
 1 file changed, 1 insertion(+)
 create mode 100644 pwd.txt
```

Les données sont actuellement sur le `local tree`, les collaborateurs n'ont pas encore accès aux modificationx et nouveaux fichiers. Pour les "pousser" sur le dépôt (`remote tree`), on utilisera la commande : `git push`

```
> git push
Counting objects: 7, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 571 bytes, done.
Total 5 (delta 2), reused 0 (delta 0)
To https://github.com/gulian/gi-git/
   42a74f2..8fe06e1  master -> master
```

#### Conflits 

Si le dépôt distant a été modifié depuis votre dernier `pull` ou `clone`, le resultat de la commande `push` sera : 

```
> git push
To https://github.com/gulian/gi-git/
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/gulian/gi-git/'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Afin de récuperer la dernière version du dépôt, utilisez la commande : `git pull`
```
> git pull
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/gulian/gi-git
   45e9a2d..42a74f2  master     -> origin/master
Merge made by the 'recursive' strategy.
 README.md | 69 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--
 1 file changed, 67 insertions(+), 2 deletions(-)
```

Le merge peut être automatique, dans ce cas là il ne vous reste plus qu'à refaire un `git push`. Dans le cas contraire, les fichiers qui n'ont pu être mergés seront marqués comme conflictueux. 



