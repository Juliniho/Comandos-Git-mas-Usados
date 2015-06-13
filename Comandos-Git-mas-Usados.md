# CONECTAR CUENTA DE USUARIO A UN REPOSITORIO #

```
#!python

git remote add origin https://<nickname | nombre_usuario>@https://bitbucket.org/titiushko/<nombre_repositorio>.git
```

# CLONAR (DESCARGAR DEL SERVIDOR) UN REPOSITORIO #

```
#!python

git clone https://<nickname | nombre_usuario>@https://bitbucket.org/titiushko/<nombre_repositorio>.git
```

# CONFIGURACION DE USUARIO #

```
#!python

git config --global user.name "<nickname | nombre_usuario>"
git config --global user.email <correo_usuario>
```

# PUSH #
- subir y actualizar todas las referencias remotas

```
#!python

git push -u origin --all
```

- subir solo la rama indicada (HEAD apunta a la rama local seleccionada) (fuente:destino)

```
#!python

git push origin HEAD:refs/for/<nombre_rama_remota>
-- otra forma
eclipse: +HEAD:refs/for/<nombre_rama_remota>
```

# FETCH #
- actualizar solo la rama indicada (fuente:destino)

```
#!python

git fetch origin refs/heads/<nombre_rama_remota>:refs/remotes/origin/<nombre_rama_local>
-- otra forma
eclipse: +refs/heads/<nombre_rama_remota>:refs/remotes/origin/<nombre_rama_local>
```

# REBASE #
- actualizar la rama seleccionada a partir de otra rama local, una rama remota o un commit

```
#!python

git rebase <nombre_rama_local | origin/nombre_rama_remota | id_commit | nombre_etiqueta>
```

# BRANCH #
### [local] ###
- crear y seleccionar

```
#!python

git checkout -b <nombre_nueva_rama_local> <nombre_rama_local | origin/nombre_rama_remota | id_commit | nombre_etiqueta>
```

- eliminar

```
#!python

git branch -D <nombre_rama_local>
```

- cambiar nombre

```
#!python

git branch -m <nombre_rama_local> <nuevo_nombre_rama_local>
```

- seleccionar

```
#!python

git checkout <nombre_rama_local>
```

- ver ramas locales

```
#!python

git branch
```

- ver ramas locales y comentario del ultimo commit de cada rama

```
#!python

git branch -v
```

- ver los datos de la rama junto con el ultimo commit en la rama

```
#!python

git show <nombre_rama_local>
```

### [remoto] ###
- crear

```
#!python

git push -f origin master:<nombre_rama_remota>
```

- eliminar

```
#!python

git push origin :<nombre_rama_remota>
-- otra forma
git push origin --delete <nombre_rama_remota>
```

- ver ramas remotas

```
#!python

git branch -r
```

- ver ramas locales y remotas

```
#!python

git branch -a
```

- ver los datos de la rama junto con el ultimo commit en la rama

```
#!python

git show remotes/origin/<nombre_rama_remota>
```

- inspeccionar un repositorio remoto

```
#!python

git remote show origin
```

# COMMIT #
### [local] ###
- agregar al commit archivos que se han modificado

```
#!python

git add <ruta completa, nombre y extencion de archivo>
```

- agregar al commit todos los archivos que se han modificado

```
#!python

git add <. | *>
```

- registrar los cambios en el repositorio realizando commit

```
#!python

git commit
```

- agregar al commit todos los archivos que se han modificado y registrar los cambios en el repositorio realizando commit

```
#!python

git commit -a
```

- agregar al commit todos los archivos que se han modificado, registrar los cambios en el repositorio realizando commit y agregar el comentario del commit

```
#!python

git commit -a -m "<comentario descriptivo del commit>"
```

- fusionar varios commits en uno solo commit

```
#!python

git reset --soft HEAD~<numero de encabezados que se quiere fusionar>
git commit -a -m "<comentario descriptivo del commit>"
```

- deshacer forzosamente todos los cambios locales

```
#!python

git reset --hard <nombre_rama_local | origin/nombre_rama_remota | id_commit | nombre_etiqueta>
```

- revertir commits

```
#!python

git reset --soft HEAD~<numero de encabezados>
```

- remover todos los archivos que se agregaron al commit

```
#!python

git reset
```

- ver los datos un commit

```
#!python

git show <id_commit>
```

### [remoto] ###
- deshacer el ultimo cambio en el repositorio remoto (commit y push)

```
#!python

git reset --hard HEAD~1
git push origin HEAD --force
```

# CLEAN #
- limpiar todos los cambios que no se incluiran en el commit

```
#!python

git checkout -- .
```

- borrar todos los archivos no versionados

```
#!python

git clean -fd
```

# TAG #
- listar todas las etiquetas disponibles con su comentario descriptivo

```
#!python

git tag
```

- crear una etiqueta anotada

```
#!python

git tag -a <nombre_etiqueta>
```

- crear una etiqueta anotada e incluir el comentario de la etiqueta

```
#!python

git tag -a <nombre_etiqueta> -m "<comentario descriptivo de la etiqueta>"
```

- eliminar una etiqueta anotada

```
#!python

git tag -d <nombre_etiqueta>
```

- ver los datos de la etiqueta junto con el commit en el que fue etiquetada

```
#!python

git show <nombre_etiqueta>
```

- subir una etiqueta al repositorio

```
#!python

git push origin <nombre_etiqueta>
```

- subir todas las etiquetas pendientes al repositorio

```
#!python

git push origin --tags
```

### [remoto] ###
- eliminar una etiqueta remota

```
#!python

git push origin :refs/tags/<nombre_etiqueta>
```

# LOG #
- mostrar la lista de todos los commits hechos en el repositorio

```
#!python

git log
```

- mostrar todas las diferencias en cada commit

```
#!python

git log -p
```

- mostrar todos los commits hechos con un archivo en especifico para ver el historial de un archivo

```
#!python

git log <ruta completa | nombre y extencion de archivo>
```

- mostrar todas las diferencias en cada commit de un archivo

```
#!python

git log -p <ruta completa | nombre y extencion de archivo>
-- otra forma
git whatchanged -p <ruta completa | nombre y extencion de archivo>
```

- mostrar la totalidad de la historia de un archivo, incluyendo la historia mas alla de renombra y con las diferencias de cada cambio

```
#!python

git log --follow -p <ruta completa | nombre y extencion de archivo>
```

- mostrar id_commit, autor, fecha + hora y linea completa de codigo para cada linea de un archivo

```
#!python

git blame <nombre y extencion de archivo>
```

# REFLOG #
- mostrar los grupos de cambios despues de reescribir la historia del estado antiguo de una rama

```
#!python

git reflog
```

- regresar a un estado o punto de la historia de una rama

```
#!python

git reset --hard HEAD@{<numero de encabezado>}
-- otra forma
git reset --hard <id_commit>
```
