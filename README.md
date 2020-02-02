# Curso Profesional de Git y GitHub

## Notas y Comandos

### Clonar

```shell
git clone $URL_O_SSH_DEL_REPOSITORIO
```

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

### Branches

```git branch nombre_de_la_rama``` crear una nueva rama con ese nombre

ver todas las branches disponibles en local

```shell
git show-branch --all
```

hacer checkout a una rama y crearla al mismo tiempo

```shell
git checkout -b branch_name
```

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

enviar los tags al repositorio en internet

```shell
git push origin --tags
```

borrar un tag en local

```shell
git tag -d $NOMBRE_DEL_TAG
```

borrar un tag en el repositorio

```shell
git push origin :refs/tags/$NOMBRE_DEL_TAG
```

### Manejo de pull/push/merge requests

en proyectos de codigo abierto el manejo del codigo con pull request es algo comun ya que permite colaborar de forma organizada y ordenada al proyecto

al hacer esto se hace necesario que tu fork del proyecto se mantenga al dia con el master por lo cual lo mejor es tener un remote aparte

agregar un remote con nombre al proyecto

```shell
git remote add $nombre_del_remote $url_o_ssh_del_proyecto
```

ademas plataformas como GitHub permiten hacer pull request desde el proyecto padre hacia tu fork, cuando el padre empieza a tener cambios que el fork no posee

### manejo con servidores

Existen servicios como:

- [Travis CI](https://travis-ci.org/) que permiten mantener al servidor actualizado constantemente, lo que haces le das accesos de git y accesos de tu servidor y cuando haya push en la rama especificada en el git, travis le hara pull en el server a los cambios. travis cuesta dinero a menos que sea un proyecto open source.

- [Jenkins](https://jenkins.io/) , este se instala en el servidor es complejo y poderoso

ambos servicios permiten aplicar integracion continua
