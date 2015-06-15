# Flujo Normal #
1. Crear una nueva ***rama local*** a partir de la rama remota ***SYSCAPv01*** del repositorio SYSCAP local. Hacer clic derecho en la rama ```Remote Trackin > origin/SYSCAPv01``` y seleccionar ```Create Branch…```.
![01.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/01.png)
2. Escribir el nombre de la nueva rama local ```SYSCAPv01-<inicial del nombre del usuario><correlativo>``` y hacer clic en el botón ```Finish```.
![02.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/02.png)
3. Trabajar en el código de SYSCAP ***sobre la rama local*** seleccionada que se creo en el paso ```2```.
![03.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/03.png)
4. Después de terminar de trabajar en el código de SYSCAP, guardar los cambios haciendo ***commit*** y agregando los archivos que se desean guardar los cambios. Hacer clic derecho sobre el repositorio SYSCAP local y seleccionar ```Commit…```.
![04.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/04.png)
5. En el área de ```Commit message``` escribir un ***comentario descriptivo que explique brevemente el porqué del cambio*** que se va a guardar, en el área ```Files (N/M)``` seleccionar los ***archivos que se incluirán en el commit*** y hacer clic en el botón ```Commit```.
![05.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/05.png)
6. Limpiar cambios que no se incluirán en el commit. Ir a la consola de comandos de Git, escribir y ejecutar los comandos ```git checkout -- .``` y ```git clean -fd```.
![13.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/13.png)
7. Verificar que se guardó el cambio. Hacer clic derecho sobre el repositorio SYSCAP local y seleccionar ```Show In/History```, o en la consola de comandos de Git, escribir y ejecutar el comando ```gitk```.
![06_1.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/06_1.png)
![06_2.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/06_2.png)
![06_3.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/06_3.png)
![06_4.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/06_4.png)
8. ***Descargar los últimos cambios*** en la rama SYSCAPv01 del ***repositorio SYSCAP remoto*** a la rama SYSCAPv01 del ***repositorio SYSCAP local***. Hacer clic derecho sobre el repositorio SYSCAP local y seleccionar ```Fetch…```.
![07.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/07.png)
9. En la ventana para hacer fecth, seleccionar que la ***fuente*** sea ```refs/heads/SYSCAPv01```, el ***destino*** sea ```refs/remotes/origin/SYSCAPv01``` y hacer clic en el botón ```Finish```.
![08.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/08.png)
10. Actualizar los cambios de la rama SYSCAPv01 del repositorio SYSCAP local a la rama local que se creó en el paso ```2```. Hacer clic derecho en la rama local ```Local > SYSCAPv01-<inicial del nombre del usuario><correlativo>``` y seleccionar ```Rebase…```.
![09.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/09.png)
11. Seleccionar la rama ```Remote Trackin > origin/SYSCAPv01``` y hacer clic al botón ```Rebase```. En caso que de ***error de conflicto*** al querer actualizar la rama local, seguir los pasos ```Alternativo```.
![10.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/10.png)
12. ***Subir los cambios*** de la rama SYSCAPv01 del repositorio SYSCAP local a la rama SYSCAPv01 del repositorio SYSCAP remoto. Hacer clic derecho sobre el repositorio SYSCAP local y seleccionar ```Push…```.
![11.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/11.png)
13. En la ventana para hacer push, seleccionar que el ***destino*** sea ```refs/heads/SYSCAPv01```, la ***fuente*** sea ```refs/heads/SYSCAPv01-<inicial del nombre del usuario><correlativo>``` y hacer clic en el botón ```Finish```.
![12.png](http://titiushko.github.io/SYSCAP/wiki/flujo-trabajo/12.png)
14. Verificar que el cambio (commit) que se acaba de subir (push) al repositorio SYSCAP remoto, aparezca en el ***historial de confirmaciones de Bitbucket***.
15. Repetir los pasos del ```1``` al ```14```.

# Flujo Alternativo #
15. De la ventana de error de conflicto, seleccionar la opción ``` ``` y hacer clic al botón ``` ```.
16. Arreglar manualmente el conflicto. Eliminar las ***líneas que agrego Git*** y guardar los cambios del archivo con conflicto.
17. Ir a la consola de comandos de Git, escribir y ejecutar el comando ```git commit -a --amend```.
18. Presionar la tecla ```Esc```, escribir ```:wq``` y presionar la tecla ```Enter```.
19. Regresar a Zend, hacer clic derecho sobre el repositorio SYSCAP local y seleccionar ```Rebase…/Continue```.
20. Continuar con el paso ```11```.