# Notas

## Comandos

### Status

```git status``` dice el status actual de archivos en git

### Reset

```git reset HEAD^``` deshace el ultimo commit sin borrar los cambios

```git reset sha_del_commit --hard``` resetea los cambios al estado anterior borrando todos los cambios locales no añadidos

```git reset sha_del_commit --soft``` resetea los cambios al estado anterior manteniedo todos los cambios locales no añadidos

### Log

```git log nombre_de_archivo``` log de los commits con cambios en ese archivo

```git log --stat``` para ver el status de los archivos cambiados por commit

### Show

```git show nombre_de_archivo``` ver cambios historicos en el archivo

```git show``` muesta el commit del ultimo cambio que hiciste

### Checkout

```git checkout sha_del_commit nombre_del_archivo``` cambio solo el archivo seleccionado a su estado en ese commit

```git checkout nombre_rama``` cambia la branch principal a la branch que se definio en el comando

### Diff

```git diff shacommit_mas_viejo shacommit_mas_nuevo``` ver cambios entre un commit y otro


### Otros

### Commits

```git commit -am``` hace commit agregando todos los cambios de archivos trackeados ( modificados ) ignorando archivos nuevos

```git commit -a``` hace lo mismo que lo anterior pero abre una consola para el mensaje del commit

### Branch

```git branch nombre_de_la_rama``` crear una nueva rama con ese nombre

### Merge

`git merge rama` fusiona la rama actual con la rama especificada

un merge es un commit en la rama donde se realiza

### solucion para unrelated histories

caso de ejemplo tienes un repo local que deseas subir a github pero al crear el repositorio de github lo iniciaste con un readme , que hacer?

`git pull origin master --allow-unrelated-histories`

ese comando permitira hacer pull al origin a pesar de que la historia de commits entre master y origin/master es distinta

### ver tus datos de usuario

`git config -l`

### Github y SSH

[Git Hub y SSH](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

### Tags

comando de crear un tag

```shell
git tag -a $NOMBRE_DEL_TAG -m "Mensaje del tag" $HASH_DEL_COMMIT
```

mostrar tag y su commit

```shell
git show-ref --tags
```
