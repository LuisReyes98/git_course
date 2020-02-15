# Curso Profesional de Git y GitHub

## Notas y Comandos

### Trackeo

git trackaera los cambios en archivos agregados, y los archivos nuevos deben ser agregados al HEAD por primera vez para iniciar el trackeo, ademas a git le importan los archivos e ignorara completamente las carpetas vacias.

### Pull y Push

Subir cambios al repostorio

`git push remote rama`

`git push origin master`

Descargar cambios del repositorio

`git pull remote rama`

`git pull origin master`

es buena practica hacer pull de manera frecuente y antes de hacer cambios

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

ver todas las ramas remotas

```shell
git branch -r
```

ver todas las ramas remotas y locales

```shell
git branch -a
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

### Ignores

No todos los archivos deberian ir a un repositorio ya sea por seguridad, porque son archivos binarios que no deberian ser guardados , son cache o son archivos autogenerados

Es mala practica guardar archivos binarios en un repositorio ya que estos deberian ser suministrados por un content delivery network.

hay pocas execepciones a esta regla como puede ser el logo del programa, pero cualquier imagen que deberia ser mandada por internet no deberia estar en el repositorio.

para ignorar estos archivos exites el `.gitignore` , el cual almacena una lista de rutas de archivos a ignorar

### README.md

este archivo :smile:, se utiliza para poder contar al historia de un proyecto de forma bonita y legible.
permite contar informacion de que es un proyecto, como funciona, que requerimientos posee entre otros.

> Muy buen curso
> - Luis Reyes

### Pages

[GitHub Pages](https://pages.github.com/) y [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/) son servicios que proveen GitLab y GitHub para publicar en un sitio web de forma gratuita un repostorio publico como una pagina web.

Este servicio permite publicar paginas web que no poseean backend.

#### Permitir que GitHub te deja crear la pagina con un home

ejemplo: `NOMBRE_REPOSITORIO.github.io` y entonces al abrir es sitio web abrirars el index.html del repositorio

para que funcione el nombre del repositorio debe ser `NOMBRE_DE_USUARIO.github.io`

### Rebase

Permite reescribir la historia de los repositorios y pegar todos los cambios de rama A a rama B, pero de tal forma como si rama jamas hubiese existido.

**ESTA ES UNA MUY MALA PRACTICA HACERLO CON RAMAS QUE ESTAN EN REPOSITORIOS REMOTOS**
por lo cual solo se deberia hacerse internamente y en repositiorios Locales.

en la rama que borras ejecutas el comando rebase para mandar sus cambios a la rama donde se fucionaran, reescribiendo la historia del repositorio

```shell
git rebase $RAMA_A_LA_CUAL_SE_UNIRAN_LOS_CAMBIOS
```

al hacer esto si la rama a la que se fusionara tiene commits mas adelante de la actual el rebase ejcutara los cambios, tambien considerar que solo funcionara cuando la rama a hacer rebase es una bifurcacion con la que se trata de unir.

es una mala practica porque cambia la historia de en que momento se creo un branch

para ejecutar el rebase, primero se hace un rebase de la rama que deseas borrar con la que uniras los cambios y depues un rebase desde la rama a la que uniras los cambios con la que desear borrar, ejemplo:

para hacer rebase de la rama `exp` en `master` se hace

```shell
(exp)$ git rebase master

(master)$ git rebase exp
```

#### Git stash

funciona para guardar cambios sin comitearlos de forma temporal

Le hace Stash a los cambios que no forman parte de un commit

```shell
git stash
```

puedes ver la lista de stash creados

```shell
git stash list
```

le haces pop al ultimo stash aplicando los cambios en la branch actual

```shell
git stash pop
```

pasar los cambios del stash a una branch nueva

```shell
git stash branch $nuevo_nombre_de_la_rama
```

borrar el ultimo stash

```shell
git stash drop
```

### Git clean

funciona para borrar archivos que no estan siendo trackeados por git, pero ignora los archivos que se ignorarian con el git ignore

para ver los archivos que git clean borrara es con

```shell
git clean --dry-run
```

para borrar los archivos que se vieron con el dry-run es con

```shell
git clean -f
```

### Cherry pick

**Usar cherry pick es una mala practica**, para pasar cambios entre ramas es mejor hacer un merge

(es de mis comandos favoritos)
es un comando util y que permite copiar un unico commit de una rama y fusionarlo en otra

copia un commit y lo fusiona con la rama actual

```shell
git cherry-pick $SHA_DEL_COMMIT
```

### Commit --amend

en ciertos casos haces un commit pero te das cuenta que no debias hacer commit aun porque faltaban, cambios por agregar.
para solucionar esto **SIN HACER PUSH** , **amend no funcionara si el commit ya esta en el repositorio remoto** ya que esto causaria conflicto de historias.

commitear los cambios en el ultimo commit

una vez los cambios se hayan agregado en el head

se fusionan estos cambios con el commit anterior con:

```shell
git commit --amend
```

### Git Reflog y Git Reset

**usar git reset es mala practica** porque borra la historia del repositorio como si los cambio nunca hubieran pasado.

si en caso de que un error masivo de archivos, se perdieron datos y no hay forma de recuperarlos con el git log, use **reflog**

Muestra la historia de **TODO** desde merge fallidos a branch borrados, orden en que se ejecutaron resets incluso estados del repositorio antes de un reset

```shell
git reflog
```

con este comando muestra la historia de acciones que han occurido en el repositorio

y usando `git reset` con el SHA de un commit de `git reflog` puedes volver en el tiempo a cualquier momento en el rpeositorio incluso a branches que ya no existen.

hacer esto es **mala practica** y solo deberia realizarse si algo se rompio en de forma tan grave que no se puede reparar y solo se puede volver en el tiempo.

### Realizar busquedas en el repositorio

buscar palabras en los archivos en el branch actual

```shell
git grep "palabra a buscar"
```

mostrar la linea en la cual la pablara aparece en el archivo

```shell
git grep -n "palabra a buscar"
```

mostrar cuantas veces aparce la palabra en cada archivo

```shell
git grep -c "palabra a buscar"
```

buscar los commits en los cuales sale una palabra

```shell
git log -S "palabra a buscar"
```

### Git rm

git rm permite borrar archivos del repositorio siempre y cuando hayan estado en staging. Es equivalente a darle click a un archivo y eliminarlo

ver el archivo que se borrara

```shell
git rm $nombre_del_archivo --dry-run
```

Borrar el archivo del disco

```shell
git rm $nombre_del_archivo
```

### Shortlog

Permite ver un historial de todos los commits por persona

```shell
git shortlog
```

muestra solamente la cantidad de commits por persona

```shell
git shortlog -sn
```

muestra la cantidad de commits (considerando todos los commits) por persona

```shell
git shortlog -sn --all
```

muestra la cantidad de commits (considerando todos los commits) sin contar los merges por persona

```shell
git shortlog -sn --all --no-merges
```

### Aliases

permite crear comandos custom de git que ejecutan otro comando de git.

**Superlog**: `git superlog`, `git log` mas bonito:

```shell
git config --global alias.superlog "log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
```

**Stats**: `git stats`, `git shortlog` mas resumido que permite ver la cantidad de commits por persona, (estadisticas):

```shell
git config --global alias.stats "shortlog -sn --all --no-merges"
```

## Proximos pasos

Sistemas de automatizacion de deployment

- [Jenkins](https://jenkins.io/)
- [Travis](https://travis-ci.org/)

Ciclo de vida DevOps de un proyecto desde:

- Testing
- Deployment
- Code Maintenance
- Constant Development Constant Deployment
- DevOps y GitLab
- Usar `git $comando --help` para conocer mas de los comandos y crear mis propios comandos custom y geniales
