Explications git
================

## Configuration

```
git config --global user.name  gulian
git config --global user.email gulian@gulian.fr
```

```
git config --global --add color.ui true
```

kikoo 

## Initialisation

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

Vous avez maintenant une copie locale du dépôt distant, et un working tree propre. Vérification avec la commande : `git status` :

```
# On branch master
nothing to commit (working directory clean)
```

(N'oubliez pas de rentrer dans le dépôt `cd gi-git`)

## Opérations de base

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

Le merge peut être automatique, dans ce cas là il ne vous reste plus qu'à refaire un `git push`. Dans le cas contraire, les fichiers qui n'ont pu être mergés seront marqués comme conflictueux:

```
> git pull
remote: Counting objects: 8, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 6 (delta 3), reused 0 (delta 0)
Unpacking objects: 100% (6/6), done.
From https://github.com/gulian/gi-git
   8fe06e1..c1c2ff0  master     -> origin/master
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Le fichiers README.md est bien marqué comme conflictueux :
```
> git status
# On branch master
# Your branch and 'origin/master' have diverged,
# and have 1 and 2 different commits each, respectively.
#
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#
#	both modified:      README.md
#
no changes added to commit (use "git add" and/or "git commit -a")
```

Etat du fichier README.md :
```
<<<<<<< HEAD
Explications du SCM Git
=====================================
=======
Explications git
================
>>>>>>> c1c2ff01a2b4f375af26b990ff37f255b8756c48
```

Après résolution du conflit :
```
> git add README.md
> git commit -m "Résolution du conflit de merge"
> git push
```

### Diff
```
> git diff
> git diff HEAD
> git diff origin/dev HEAD
> git diff origin/master HEAD
> git diff origin/dev 4c1692395de7285e3ad83155542fabd02cf94838
```


### Suppression d'un fichier
```
> git rm pwd.txt
> git commit -m "En fait on s'en *$#&## de ce fichier"
> git push
```

> D'autres fonctions sont dispo et ressemble aux commande UNIX (git rm, git mv etc.)

### Restauration d'un fichier (retour à l'état du dépôt local)
```
> git checkout -- README.md
```

### Restauration de tout le dépôt

> Attention : Remplace tout le depôt local par le dépôt distant

```
> git reset --hard origin/master
HEAD is now at 1ecb57e Merge branch 'master' of https://github.com/gulian/gi-git
```


### Stash (mettre son travail de côté) : `git stash`

La commande `git stash` va mettre toutes les modifications non commitées en attente sur une pile pour rendre votre dépôt clean. Pratique quand on vous demande une correction TRES TRES URGENTE et que vous ne pouvez pas vous permettre de commiter votre travail en l'état.

```
> git stash
### correction TRES TRES URGENTE
> git stash apply
```

Ceci restaurera le dernier stash. Vous pouvez empiler les stashs et les visionner grâce à la commande `git stash list` (extrait de smartgeomobile) :
```
stash@{1}: WIP on master: 39a6a38 remove useless files
stash@{2}: WIP on master: bb8f786 Update config.xml
stash@{3}: WIP on master: 0070341 Merge branch 'master' of https://github.com/gismartwaredev/smartgeomobile
stash@{4}: WIP on master: 2505583 Fixes zone's edge 4pixels line width
stash@{5}: WIP on master: cbe7e24 add spinner to report (closes #90)
```

Cette liste n'est qu'une suite de commit sur lequel vous avez stashé. Pour être plus parlant vous pouvez donner un nom à vos stashs. Par exemple:
```
> git stash save "Avant que le chef vienne me demander de"
### la fameuse requête du chef
> git stash list
stash@{1}: Avant que le chef vienne me demander de
> git stash apply stash@{1}
```

## Branching

### Création d'une branche
```
> git branch features/awesomeness
> git checkout features/awesomeness
Switched to branch 'features/awesomeness'
> echo ":)" >> smiley.txt
> git add smiley.txt
> git commit -m ":) :shipit:"
> git push -u origin feature/awesomeness
Counting objects: 39, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (34/34), done.
Writing objects: 100% (39/39), 9.00 KiB, done.
Total 39 (delta 15), reused 0 (delta 0)
To https://github.com/gulian/gi-git/
 * [new branch]      features/awesomeness -> features/awesomeness
```
L'option `-u` permet de specifier sur quelle branche on risque de travailler pendant un moment. La prochaine fois pour pousser on utilisera juste `git push`. Et quand on reviendra sur le master on utilisera `git push -u origin master`.


### Merge d'une branche
```
> git checkout master
Switched to branch 'master'
> git merge features/awesomeness
Updating e8c0f7f..ed9b831
Fast-forward
 smiley.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 smiley.txt
> git push -u origin master
```

### Suppresion d'une branche

#### Locale
```
> git branch -d features/awesomeness
Deleted branch features/awesomeness (was ed9b831).
```

#### Distante
```
> git push origin :features/awesomeness
To https://github.com/gulian/gi-git/
 - [deleted]         features/awesomeness
```

## Les trucs en plus :+1:

```
git bisect
git rebase
git log
git checkout -
git config --global alias.graph "log --graph --all --pretty=format:'%Cred%h%Creset - %Cgreen(%cr)%Creset %s%C(yellow)%d%Creset' --abbrev-commit --date=relative"
```
lol :poo:
