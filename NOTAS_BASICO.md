# Notas

## Commandos

### git reset

reseta los cambios pero los deja en el working directorie solo hace falta hacer commit
```git reset --soft [commit]```.

resetea los cambios y los quita del working direcorie hay que hacer ```git add``` una vez mas
```git reset --mixed [commit]```

retorna el head un commit deshaciendo el ultimo commit
comando muy util, resetear ultimo commit sin borrar los cambios

```shell
git reset HEAD^
```

### git log

Muestra todos los commit incluso tras un reset hard

```shell
git log --reflog
```

Muestra el log con diffs

```shell
git log -p
```

### GIT SUPERLOG

```shell
git config --global alias.superlog "log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
```

### Configurar variables de git

```shell
git config --global #variable de forma global

git config --local #variable solo en este repositorio
```

### Configurar vs code como editor

```shell
git config --global core.editor "code --wait"
```

### Crear ramas

```shell
git brach [nombre]
```

### Cambiar nombre de ramas

```shell
git branch -m responsive RD

```

### checkout

```shell
git checkout [branch name | commit]
```

### merge

teniendo dos ramas debo hacer checkout a la rama que quiero que reciba los datos 
y luego

```shell
git merge [branch name]
```

git merge [rama]: Nos permite mezclar los cambios realizados en dicha rama con la rama en la que estamos.

fast-forward: los mezcla automáticamente
recursive/auto-merging: ambas ramas salieron al mismo tiempo y hay algo nuevo en la rama que la otra no recuerda, por eso hace la mezcla recursiva.
manual merge: nos va a tocar decirle a git específicamente los cambios que queremos mezclar

### git rebase

es peligroso y solo deberia aplicarse en local

git rebase: hace prácticamente lo mismo que merge, cambiamos la historia de nuestro proyecto sin crear bifurcaciones del proyecto. Es mejor usar merge
Usar solo git rebase de manera local.

```shell
git rebase [branch name]
```

-i: de manera interactiva, nos abrira el editor que tengamos definido en la configuración de git.

```shell
git rebase -i [branch name]
```

### git cherry-pick

Te permite extraer un unico commit y aplicar sus cambios en la rama actual

```shell
git cherry-pick [commit hash]
```

## Exclusivos de Git Hub y Git Lab

### remote

Añadir primer remoto

```shell
git remote add origin [ssh/https]
```

ver version

```shell
git remote -v
```

eleminar remote

```shell
git remote remove [name]
```

### pull y fetch

traer datos con pull

```shell
git pull origin master
```

traer datos con fetch

```shell
git fetch origin master
```

y luego

```shell
git merge origin/master
```

### push

------

Asi subimos nuestros cambios a github:

```shell
git push origin master
```

Tambien podemos enviar los tags:

```shell
git push origin master --tags
```

Podemos enviar otras ramas:

```shell
git push origin [otra_rama]
```
