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

### Checkout

```git checkout sha_del_commit nombre_del_archivo``` cambio solo el archivo seleccionado a su estado en ese commit

### Diff

```git diff shacommit_mas_viejo shacommit_mas_nuevo``` ver cambios entre un commit y otro

### Otros

### Commits

```git commit -am``` hace commit agregando todos los cambios de archivos trackeados ( modificados ) ignorando archivos nuevos

```git commit -a``` hace lo mismo que lo anterior pero abre una consola para el mensaje del commit
