# Git y GitHub

> Pruebe en lugar de argumentar. - Proverbio japonés

## ¿Qué son Git y GitHub?

Git es un programa de línea de comandos que le permite rastrear versiones de cualquier código o
documento de texto plano que usted cree. Al igual que la función "Control de cambios" de
un procesador de textos, Git realiza un seguimiento de quién hizo cambios particulares, el tiempo y
fecha de esos cambios y dónde se realizaron los cambios. Si un archivo crucial
se borra por accidente, o si hace un cambio radical a su código y desea
intentar descubrir dónde se realizó el cambio, puede usar Git para
restaurar el archivo eliminado o encontrar el nuevo error en su programa. Git organiza
grupos de archivos que está rastreando en un **repositorio**, que es solo un
directorio donde se rastrean todos los cambios en los archivos en ese directorio. Git
también puede ayudarlo a colaborar con otros cuando está escribiendo software. Como 
[Karl Broman](https://twitter.com/kwbroman) dice
(parafraseando a [Mark Holder](https://twitter.com/mtholder)):
"Su colaborador más cercano es usted hace seis meses, pero que no responde
correos electrónicos"

GitHub es un sitio web que proporciona repositorios remotos de Git. Un repositorio remoto
es solo un repositorio de Git al que puede acceder a través de una conexión a Internet.
GitHub le permite crear repositorios remotos públicos de forma gratuita, y cualquiera puede
ver su código en estos repositorios públicos. Si quiere mantener su código privado
entonces puedes pagar GitHub por repositorios remotos privados.

Si está trabajando
en el código junto con un amigo, GitHub puede ayudarlo a sincronizar los cambios en los archivos de código
entre usted y su amigo. También hay un aspecto social y comunitario en
GitHub, ya que puede ver a otros programadores desarrollar sus proyectos. GitHub
también hace que sea fácil venir en la ayuda de alguien con su proyecto. GitHub
ofrece muchas otras características útiles que se discutirán extensamente.

## Configurando Git y GitHub

Antes de configurar Git, vaya a [GitHub](https://github.com/) y cree una cuenta
gratis. Tome nota de la dirección de correo electrónico que usa y el nombre de usuario que elija.

Para ver si tiene instalado Git abra su terminal e ingrese lo siguiente:

```
git --version
```

Si no recibe una respuesta diciéndole la versión de Git que tiene instalada entonces necesita instalar Git. Puede encontrar instrucciones para instalar Git en tu sistema operativo
[here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

Abra su shell una vez que haya instalado git y ejecute `git --version` nuevamente para
asegúrarse de que la instalación sea exitosa (es posible que deba reiniciar su shell o
su computadora). Después de instalar Git, debemos configurar dos
variables, pero solo necesitamos hacer esto una vez. La primera variable que necesitamos establecer
con Git es su nombre de usuario GitHub, y la segunda variable es el correo electrónico
que utilizó para crear su cuenta de GitHub:


```{r, engine='bash', eval=FALSE}
git config --global user.name "myUserName"
git config --global user.email myName@email.com
```


## Comenzando con Git

Vamos a crear nuestro primer repositorio de Git. Primero tenemos que crear un directorio:

```{r, engine='bash', eval=FALSE}
cd
mkdir my-first-repo
cd my-first-repo
```

"Repo" en este caso es solo una abreviatura de "repositorio". Para comenzar a rastrear archivos con Git en un directorio, ingresa `git init` en la línea de comandos:

```{r, engine='bash', eval=FALSE}
git init
```

```
## Initialized empty Git repository in /Users/Martin/my-first-repo/.git/
```

¡Acaba de crear su primer repositorio! Ahora vamos a crear un archivo y a comenzar
a rastrearlo

```{r, engine='bash', eval=FALSE}
echo "Welcome to My First Repo" > readme.txt
```

Ahora que hemos creado un archivo en este repositorio de Git, usemos `git status` para
ver qué está pasando en este repositorio. Usaremos `git status` continuamente
a lo largo de este gist para obtener información sobre el estado de este repositorio de Git.

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
##
## Initial commit
##
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
## 	readme.txt
##
## nothing added to commit but untracked files present (use "git add" to track)
```

Como puede ver, `readme.txt` se muestra como un archivo sin seguimiento. Para hacer que Git
sepa que quiere rastrear este archivo, necesitamos usar `git add` con el nombre de
el archivo que queremos rastrear. Comencemos rastreando `readme.txt`:

```{r, engine='bash', eval=FALSE}
git add readme.txt
```

Git ahora sabe rastrear cualquier cambio a `readme.txt`. Veamos cómo el estado de
el repositorio ha cambiado:

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
##
## Initial commit
##
## Changes to be committed:
##   (use "git rm --cached <file>..." to unstage)
##
## 	new file:   readme.txt
##
```

Git ahora está rastreando `readme.txt`, o en el lenguaje específico de Git `readme.txt` está
ahora **staged**. Entre los paréntesis en el mensaje de arriba puede ver que
`git status` nos da un consejo sobre cómo unstaged (o dejar de preparar) este archivo,
lo cual podríamos hacer con `git rm --cached readme.txt`. Vamos a dejar de preparar este archivo solo para ver que pasa:

```{r, engine='bash', eval=FALSE}
git rm --cached readme.txt
```

```
## rm 'readme.txt'
```

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
##
## Initial commit
##
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
## 	readme.txt
##
```

Nuestro repositorio vuelve a la forma en que comenzó con `readme.txt` como un
archivo sin preparar. Comencemos rastreando `readme.txt` nuevamente para poder pasar a
características más importantes de Git.

```{r, engine='bash', eval=FALSE}
git add readme.txt
```

Ahora que Git está rastreando `readme.txt` necesitamos crear un hito para indicar
los cambios que hicimos a `readme.txt`. En este caso, los cambios que hicimos
estaban creando el archivo en primer lugar! Este hito se llama **commit**
en Git. Un commit registra el contenido de todos los archivos que están preparados. Ahora sólo tenemos `readme.txt` preparadp, así que vamos a confirmar la creación de este archivo.
Al hacer una confirmación en Git, necesitamos escribir un mensaje de confirmación que se especifica después de la etiqueta `-m`. El mensaje debe describir brevemente qué cambios has
hecho desde el último commit.

```{r, engine='bash', eval=FALSE}
git commit -m "added readme.txt"
```

```
## [master (root-commit) 73e53ca] added readme.txt
##  1 file changed, 1 insertion(+)
##  create mode 100644 readme.txt
```

El mensaje anterior confirma que el commit tuvo éxito y resume los
cambios que tuvieron lugar desde el último commit. Como puede ver en el mensaje,
solo cambiamos un archivo, y solo cambiamos una línea en ese archivo. Corramos
`git status` nuevamente para ver el estado de nuestro repositorio después de que hayamos hecho el primer commit:

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
## nothing to commit, working tree clean
```

¡Todos los cambios a los archivos en este repositorio han sido confirmados! Vamos a
agregar algunos archivos más a este repositorio y confirmarlos.

```{r, engine='bash', eval=FALSE}
touch file1.txt
touch fil2.txt
ls
```

```
## file1.txt
## fil2.txt
## readme.txt
```

Mientras estamos en eso, agreguemos una nueva línea de texto a `readme.txt`:


```{r, engine='bash', eval=FALSE}
echo "Learning Git is going well so far." >> readme.txt
```

Ahora que hemos agregado dos archivos más y hemos realizado cambios en un archivo, vamos a
echar un vistazo al estado de este repositorio.

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
##
## 	modified:   readme.txt
##
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
## 	fil2.txt
## 	file1.txt
##
## no changes added to commit (use "git add" and/or "git commit -a")
```

Podemos ver que Git ha detectado que un archivo ha sido modificado y que hay dos archivos en este directorio que no están siendo rastreados. Ahora tenemos que decirle a
Git que rastree los cambios a estos archivos. Podríamos decirle a Git que rastree los cambios en
cada archivo usando `git add`, o dado que todos los archivos en este repositorio son
`.txt` archivos podríamos usar un comodín e ingresar` git add * .txt` en la
consola. Sin embargo, si queremos hacer un seguimiento de todos los cambios en todos los archivos en
nuestro directorio deberíamos usar el comando `git add -A`.

```{r, engine='bash', eval=FALSE}
git add -A
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
##
## 	new file:   fil2.txt
## 	new file:   file1.txt
## 	modified:   readme.txt
##
```

Ahora se están rastreando los cambios a todos los archivos en este repositorio.
Finalmente, confirmemos estos cambios:

```{r, engine='bash', eval=FALSE}
git commit -m "added two files"
```

```
## [master 53a1983] added two files
##  3 files changed, 1 insertion(+)
##  create mode 100644 fil2.txt
##  create mode 100644 file1.txt
```

¡Demonios!, ahora mirando este resumen de confirmación me doy cuenta de que tengo un error tipográfico en uno
de los nombres de mis archivos! Afortunadamente, podemos deshacer el commit más reciente con
el comando `git reset --soft HEAD~`:

```{r, engine='bash', eval=FALSE}
git reset --soft HEAD~
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
##
## 	new file:   fil2.txt
## 	new file:   file1.txt
## 	modified:   readme.txt
##
```

Este repositorio ahora se encuentra exactamente en el mismo estado en el que estaba antes de que hiciéramos el
commit. Ahora podemos cambiar el nombre de `fil2.txt` a `file2.txt`, entonces veamos el
estado del repositorio de nuevo.

```{r, engine='bash', eval=FALSE}
mv fil2.txt file2.txt
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
##
## 	new file:   fil2.txt
## 	new file:   file1.txt
## 	modified:   readme.txt
##
## Changes not staged for commit:
##   (use "git add/rm <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
##
## 	deleted:    fil2.txt
##
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
## 	file2.txt
##
```

Le dijimos previamente a Git que rastreara `fil2.txt`, y podemos ver que Git reconoce
que el archivo ha sido eliminado. Podemos poner a Git al tanto de qué archivos
debería estar siguiendo con `git add -A`:

```{r, engine='bash', eval=FALSE}
git add -A
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
##
## 	new file:   file1.txt
## 	new file:   file2.txt
## 	modified:   readme.txt
##
```

¡Finalmente tenemos los nombres de los archivos correctos! Ahora hagamos el commit correcto:

```{r, engine='bash', eval=FALSE}
git commit -m "added two files"
```

```
## [master 12bb9f5] added two files
##  3 files changed, 1 insertion(+)
##  create mode 100644 file1.txt
##  create mode 100644 file2.txt
```

Se ve mucho mejor.

### Resumen

- Git sigue los cambios a los archivos de texto plano (archivos de código y documentos de texto).
- Un directorio donde los cambios son seguidos por Git se llama
repositorio de Git.
- Cambie su directorio de trabajo, luego ejecute `git init` para iniciar un repositorio.
- Puede rastrear los cambios a un archivo usando `git add [nombres de archivos]`.
- Puede crear un hito sobre el estado de sus archivos utilizando el mensaje `git commit -m 'mensaje sobre los cambios desde la última confirmación" `.
- Para examinar el estado de los archivos en su repositorio use `git status`.

### Ejercicios

1. Inicie un repositorio en un nuevo directorio.
2. Cree un nuevo archivo en su nuevo repositorio de Git. Asegúrese de que Git está rastreando
el archivo y luego cree una nueva confirmación.
3. Realice cambios en el archivo y luego confirme estos cambios.
4. Agregue dos archivos nuevos a su repositorio, pero solo confirme uno de ellos. ¿Cuál es
el estado de su repositorio después de la confirmación?
5. Deshaga la última confirmación, agregue el archivo sin seguimiento y vuelva a realizar la confirmación.


## Características importantes de Git

### Ayuda, registros y diferencias

Los comandos de Git tienen sus propios manuales 'man'. Puede acceder a ellos con
`git help [nombre del comando]`. Por ejemplo, aquí está el comienzo de la página de ayuda
para `git status`:

```{r, engine='bash', eval=FALSE}
git help status
```

```
GIT-STATUS(1)                                Git Manual                               GIT-STATUS(1)

NAME
       git-status - Show the working tree status

SYNOPSIS
       git status [<options>...] [--] [<pathspec>...]

DESCRIPTION
       Displays paths that have differences between the index file and the current HEAD commit,
       paths that have differences between the working tree and the index file, and paths in the
       working tree that are not tracked by Git (and are not ignored by gitignore(5)). The first
       are what you would commit by running git commit; the second and third are what you could
       commit by running git add before running git commit.
```

Al igual que cualquier otra página de ayuda que use `less`, puede volver al prompt
con la tecla `Q`.

Si desea ver una lista de sus commits de Git, ingrese `git log` en la consola:

```{r, engine='bash', eval=FALSE}
git log
```

```
## commit 12bb9f53b10c9b720dac8441e8624370e4e071b6
## Author: seankross <sean@seankross.com>
## Date:   Fri Apr 21 15:23:59 2017 -0400
##
##     added two files
##
## commit 73e53cae75301ce9b2802107b1956447241bb17a
## Author: seankross <sean@seankross.com>
## Date:   Thu Apr 20 14:15:26 2017 -0400
##
##     added readme.txt
```

Si ha realizado muchos commits en un repositorio, es posible que deba presionar la tecla `Q`
para volver al prompt. Cada commit tiene su hora, fecha y mensaje de confirmación
grabado, junto con un hash SHA-1 que identifica de manera única la confirmación.

Git también puede ayudar a mostrar las diferencias entre los cambios no registrados en sus archivos
comparado con el último commit. Agreguemos una nueva línea de texto a `readme.txt`:

```{r, engine='bash', eval=FALSE}
echo "The third line." >> readme.txt
git diff readme.txt
```

```
## diff --git a/readme.txt b/readme.txt
## index b965f6a..a3db358 100644
## --- a/readme.txt
## +++ b/readme.txt
## @@ -1,2 +1,3 @@
##  Welcome to My First Repo
##  Learning Git is going well so far.
## +I added a line.
```

Como puede ver, aparece un signo más al lado de la línea agregada. Ahora vamos a abrir
este archivo en un editor de texto para que podamos eliminar la segunda línea.

```{r, engine='bash', eval=FALSE}
nano readme.txt
# Borrar la segunda línea
git diff readme.txt
```

```
## diff --git a/readme.txt b/readme.txt
## index b965f6a..e173fdf 100644
## --- a/readme.txt
## +++ b/readme.txt
## @@ -1,2 +1,2 @@
##  Welcome to My First Repo
## -Learning Git is going well so far.
## +I added a line.
```

Aparece un signo menos al lado de la línea que eliminamos. Echemos un vistazo a la
estado de nuestro directorio en este punto.

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
##
## 	modified:   readme.txt
##
## no changes added to commit (use "git add" and/or "git commit -a")
```

Si lee detenidamente los resultados de `git status`, puede ver que podemos tomar
este repositorio en una de dos direcciones en este punto. Podemos o bien hacer `git add`
a los archivos que le hemos realizado cambios para rastrear esos cambios, o podemos
usar `git checkout` para eliminar todos los cambios que hemos realizado en un archivo
para restaurar su contenido a lo que estaba presente en el último commit. Vamos a eliminar
nuestros cambios para ver cómo funciona esto.

```{r, engine='bash', eval=FALSE}
cat readme.txt
```

```
## Welcome to My First Repo
## I added a line.
```

```{r, engine='bash', eval=FALSE}
git checkout readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
```

Como puede ver, los cambios que le hicimos a `readme.txt` han sido deshechos.

### Ignorar archivos

A veces podemos tener archivos que nunca deseamos que Git rastree, por ejemplo
archivos binarios que se generan como subproductos del código en ejecución (archivos PDF o imágenes),
o secretos como contraseñas o claves API. Un archivo en su repositorio de Git llamado
`.gitignore` puede mostrar los nombres de los archivos y subcarpetas, o simplemente
expresiones regulares (lo que se puede usar con `ls`) para especificar archivos que
nunca deben ser rastreados. Cada línea de un archivo `.gitignore` debe especificar un archivo
o un grupo de archivos que Git no debe rastrear. Hagamos un archivo `.gitignore`
para asegurarnos de que nunca rastreamos los archivos de imagen en este repositorio:

```{r, engine='bash', eval=FALSE}
touch toby.jpg
git status
```

```
## On branch master
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
## 	toby.jpg
##
## nothing added to commit but untracked files present (use "git add" to track)
```

Ahora que hemos agregado una imagen a nuestro repositorio, agreguemos un archivo `.gitignore`
para asegurarnos de que Git no rastree este tipo de archivos.

```{r, engine='bash', eval=FALSE}
echo "*.jpg" > .gitignore
git status
```

```
## On branch master
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
## 	.gitignore
##
## nothing added to commit but untracked files present (use "git add" to track)
```

Ahora podemos ver que Git ha detectado el nuevo archivo `.gitignore`, pero no 
ve `toby.jpg`. Vamos a agregar y confirmar nuestro archivo `.gitignore`:

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "added gitignore"
```

```
## [master adef548] added gitignore
##  1 file changed, 1 insertion(+)
##  create mode 100644 .gitignore
```

Ahora si agregamos otro archivo `.jpg`, Git no verá el archivo:

```{r, engine='bash', eval=FALSE}
touch bernie.jpg
git status
```

```
## On branch master
## nothing to commit, working tree clean
```

```{r, engine='bash', eval=FALSE}
ls
```

```
## bernie.jpg
## toby.jpg
## file1.txt
## file2.txt
## readme.txt
```

### Resumen

- `git help` le permite leer las páginas `man` para comandos específicos de Git.
- `git log` le mostrará su historial de commits.
- `git diff` muestra qué ha cambiado entre el último commit y los
cambios sin seguimiento actuales.
- Puede especificar un archivo `.gitignore` para decirle a Git que no rastree ciertos
archivos.

### Ejercicios

1. Mire las páginas de ayuda para `git log` y `git diff`.
2. Agregue al `.gitignore` que ya comenzó a incluir, un nombre de archivo específico,
luego agregue ese archivo a su repositorio.
3. Cree un archivo que contenga el registro de Git para este repositorio. Use `grep` para
ver en qué día de la semana ocurrieron la mayoría de las confirmaciones.

## Branching

La ramificación es una de las características más poderosas que ofrece Git. Crear
diferentes branches de Git le permite trabajar en una característica particular o conjunto de
archivos independientemente de otras "copias" de un repositorio. De esa manera usted y un
amigo puede trabajar en diferentes partes del mismo archivo en diferentes ramas, y
luego Git puede ayudarle a fusionar elegantemente sus ramas y cambios juntos.

Puede listar todas las ramas disponibles con el comando `git branch`:

```{r, engine='bash', eval=FALSE}
git branch
```

```
## * master
```

La estrella (`*`) indica en qué rama se encuentra actualmente. La rama predeterminada
que se crea siempre se llama *master*. Por lo general, las personas usan esta rama como la
versión de trabajo del software que están escribiendo, mientras desarrollan características nuevas y potencialmente inestables en otras ramas.

Para agregar una rama también usaremos el comando `git branch`, seguido del nombre de
la rama que queremos crear:

```{r, engine='bash', eval=FALSE}
git branch my-new-feature
```

Ahora ingresemos `git branch` nuevamente para confirmar que hemos creado la rama:

```{r, engine='bash', eval=FALSE}
git branch
```

```
## * master
## my-new-feature
```

Podemos hacer de `my-new-feature` la rama actual usando `git checkout` con el
nombre del branch:

```{r, engine='bash', eval=FALSE}
git checkout my-new-feature
```

```
## Switched to branch 'my-new-feature'
```

```{r, engine='bash', eval=FALSE}
git branch
```

```
##   master
## * my-new-feature
```

Si observamos el `git status` también podemos ver que nos dirá en qué rama
estamos:


```{r, engine='bash', eval=FALSE}
git status
```

```
On branch my-new-feature
nothing to commit, working tree clean
```

Podemos volver a la rama `master` usando `git checkout`:

```{r, engine='bash', eval=FALSE}
git checkout master
```

```
## Switched to branch 'master'
```

```{r, engine='bash', eval=FALSE}
git branch
```

```
## * master
##   my-new-feature
```

Ahora podemos eliminar una rama usando la etiqueta `-d` con `git branch` y el nombre
de la rama que queremos eliminar:

```{r, engine='bash', eval=FALSE}
git branch -d my-new-feature
```

```
## Deleted branch my-new-feature (was adef548).
```

```{r, engine='bash', eval=FALSE}
git branch
```

```
## * master
```

Creemos una nueva rama para agregar una sección al `readme.txt` en nuestra
repositorio. Podemos crear una nueva rama y cambiar a esa rama al mismo
tiempo usando el comando `git checkout -b` y el nombre de la nueva rama que queremos
crear:


```{r, engine='bash', eval=FALSE}
git checkout -b update-readme
```

```
## Switched to a new branch 'update-readme'
```

Ahora que hemos creado y cambiado a una nueva rama, hagamos algunos cambios en
un archivo. Como podríamos estar esperando ahora, agregaremos una nueva línea para
`readme.txt`:

```{r, engine='bash', eval=FALSE}
echo "I added this line in the update-readme branch." >> readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
```

Ahora que hemos agregado una nueva línea, confirmemos estos cambios:

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "added a third line to readme.txt"
```

```
## [update-readme 6e378a9] added a third line to readme.txt
##  1 file changed, 1 insertion(+)
```

Ahora que hemos hecho una confirmación en la rama `update-readme`, volvamos a la rama
`master`, y luego echemos un vistazo a `readme.txt`:

```{r, engine='bash', eval=FALSE}
git checkout master
```

```
## Switched to branch 'master'
```

Ahora que estamos en la rama `master`, echemos un vistazo rápidamente a `readme.txt`:


```{r, engine='bash', eval=FALSE}
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
```

¡La tercera línea que agregamos se ha ido! No se preocupe, la línea que agregamos no
se fue para siempre. Hemos confirmado el cambio en este archivo mientras estábamos en la rama
`update-readme`, por lo que el archivo actualizado está en esa rama. Vamos a
volver a esa rama solo para asegurarnos:

```{r, engine='bash', eval=FALSE}
git checkout update-readme
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
```

¡Y la tercera línea está de vuelta! Vamos a agregar y confirmar otra línea más mientras estamos en esta rama:

```{r, engine='bash', eval=FALSE}
echo "It's sunny outside today." >> readme.txt
git add -A
git commit -m "added weather info"
```

```
## [update-readme d7946e9] added weather info
##  1 file changed, 1 insertion(+)
```

Este es un pequeño ejemplo de cómo usar la ramificación de Git, pero se puede ver cómo
puede realizar ediciones incrementales en texto sin formato (generalmente archivos de código) sin que tengan efecto en la rama `master` (la copia probada y funcional de su software)
y sin afectar otras ramas. Puede imaginar cómo
este sistema podría usarse para que varias personas trabajen en la misma base de código
al mismo tiempo, o cómo podría desarrollar y probar múltiples funciones en un software
sin que ellos interfieran entre sí. Ahora que hemos hecho un par de
cambios en `readme.txt`, combinemos esos cambios con lo que tenemos en
rama `master`. Esto es posible gracias a un **merge**  de Git. `merge` le permite
combinar elegantemente los cambios que se han realizado entre dos ramas. Vamos a
fusionar los cambios que hicimos en la rama `update-readme` con la rama`master`. Git incorpora otras ramas en la rama actual de forma predeterminada.
Cuando se fusiona, la rama actual también se denomina rama **base**.
Cambiemos a la rama `master` para que podamos combinar los cambios de la rama
`update-readme`:

```{r, engine='bash', eval=FALSE}
git checkout master
```

```
## Switched to branch 'master'
```

Para combinar los cambios desde otra rama, necesitamos usar `git merge` y
nombre de la rama:

```{r, engine='bash', eval=FALSE}
git merge update-readme
```

```
## Updating adef548..d7946e9
## Fast-forward
##  readme.txt | 2 ++
##  1 file changed, 2 insertions(+)
```

```{r, engine='bash', eval=FALSE}
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's sunny outside today.
```

¡Parece que fusionó su primera rama en Git! La ramificación es parte de lo
que hace que Git sea tan poderoso ya que permite desarrollos paralelos en el mismo código
base. Pero ¿y si hay dos commits en dos ramas separadas que hacen
diferentes ediciones a la misma línea de texto? Cuando esto ocurre, se llama
**conflict**. Vamos a crear un conflicto para que podamos aprender cómo se pueden resolver.

Primero cambiaremos a la rama `update-readme`. Use `nano` para editar la última
línea de `readme.txt`, luego confirme sus cambios:

```{r, engine='bash', eval=FALSE}
git checkout update-readme
nano readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's cloudy outside today.
```

Observe que cambiamos "summy" a "cloudy" en la última línea.

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "changed sunny to cloudy"
```

Ahora que nuestros cambios están confirmados en la rama `update-readme`, cambiemos
a `master`:

```{r, engine='bash', eval=FALSE}
git checkout master
```

Cambiemos la misma línea de código usando `nano`:

```{r, engine='bash', eval=FALSE}
nano readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's windy outside today.
```

Ahora confirmemos estos cambios:

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "changed sunny to windy"
```

Ahora hemos creado dos commits que entran en conflicto directamente entre sí. Sobre el branch
`update-readme`, la última línea dice `It's cloudy outside today`, mientras
en la rama `master`, la última línea dice `It's windy outside today`. Vamos a
mirar qué sucede cuando tratamos de combinar `update-readme` en` master`.

```{r, engine='bash', eval=FALSE}
git merge update-readme
```

```
## Auto-merging readme.txt
## CONFLICT (content): Merge conflict in readme.txt
## Automatic merge failed; fix conflicts and then commit the result.
```

¡Wow, hay un conflicto! Vamos a verificar el estado del repositorio en este momento:

```{r, engine='bash', eval=FALSE}
git status
```

```
## On branch master
## You have unmerged paths.
##   (fix conflicts and run "git commit")
##   (use "git merge --abort" to abort the merge)
##
## Unmerged paths:
##   (use "git add <file>..." to mark resolution)
##
## 	both modified:   readme.txt
##
## no changes added to commit (use "git add" and/or "git commit -a")
```

Si se está acostumbrando a leer el resultado del `git status`, puede ver que
a menudo ofrece sugerencias sobre qué pasos debe seguir. Git está
indicando que ambas versiones de readme.txt han modificado el mismo texto. Vamos a
echar un vistazo a `readme.txt` para ver qué está pasando allí:

```{r, engine='bash', eval=FALSE}
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## <<<<<<< HEAD
## It's windy outside today.
## =======
## It's cloudy outside today.
## >>>>>>> update-readme
```

Las primeras tres líneas de este archivo se ven normales, ¡entonces las cosas se ponen interesantes!
La línea entre `<<<<<<< HEAD` y `======= `muestra la versión de la
línea conflictiva en la rama actual. En la terminología de Git el `HEAD`
representa la confirmación más reciente en la rama en que está actualmente
(que es `master` en este caso). La línea entre `=======` y
`>>>>>>> update-readme` muestra la versión de la línea en la rama `update-readme`. Para resolver este conflicto, todo lo que tenemos que hacer es abrir `readme.txt`
con `nano` para poder eliminar las líneas de las que queremos deshacernos. En este caso, vamos a mantener la versión "cloudy".

```{r, engine='bash', eval=FALSE}
nano readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's cloudy outside today.
```

Ahora podemos comprometer la resolución de este conflicto.

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "resolved conflict"
```

¡Ahora está familiarizado con estos conceptos básicos de Git! Si quiers entrar más en
profundidad con el estudio de Git le recomiendo el libro de código abierto y gratuito
[Pro Git](https://git-scm.com/book/).

### Resumen

- La ramificación de Git le permite a usted y a otros trabajar juntos en la misma base de códigos.
- Puede crear una rama con el comando `git branch [nombre de la rama]`.
- Para cambiar a otra rama use `git checkout [nombre de la rama]`.
- Puede combinar una rama con su rama actual usando `git merge`.

### Ejercicios

1. Cree una nueva rama.
2. Cambie a esa rama y agregue commits a ella. Cambie a una rama más antigua y
luego fusione la nueva rama en su rama actual.
3. Cree y resuelva a propósito un conflicto de fusión.

## GitHub

Ahora que conoce los conceptos básicos del uso de Git, hablemos sobre cómo puede compartir
su trabajo y comience a colaborar en línea usando GitHub. 
Para comenzar, vaya a [GitHub](https://github.com/) e inicie sesión con las
credenciales que configuramos al comienzo del capítulo. Después de iniciar sesión
debería ver un signo más cerca de la esquina superior derecha de su navegador web. Haga clic en el
signo más y un pequeño menú debe aparecer, luego haga clic en "New repository".

En el cuadro de texto debajo de **Repository Name**, escriba `my-first-repo` y luego haga clic en el botón verde **Create repository**.

GitHub ofrece algunas sugerencias sobre qué hacer con nuestro nuevo repositorio remoto.
Ya hemos estado usando un repositorio local de Git, y lo que GitHub proporciona es un
 repositorio **remoto** de Git. Un repositorio remoto de Git es solo un repositorio de Git
almacenado en una computadora que siempre está encendida y conectada a internet, por lo que
puede actuar como un punto central donde podemos compartir y sincronizar nuestros cambios a los archivos
con nuestros amigos y colegas. Podemos ver a qué repositorios remotos está conectado nuestro
repositorio local con el comando `git remote` mientras tenemos nuestro
directorio de trabajo establecido en `my-first-repo`:

```{r, engine='bash', eval=FALSE}
git remote
```

No se imprime nada en la consola ya que aún no ha configurado ningún control remoto aún.
Ahora agreguemos su nuevo repositorio de GitHub como un control remoto en su repositorio local:

```{r, engine='bash', eval=FALSE}
git remote add origin https://github.com/seankross/my-first-repo.git
```

En el comando de arriba `git remote add` agregue un nuevo control remoto a su repositorio local,
`origin` es el nombre que asignamos a este repositorio remoto, y
`https://github.com/mamaciasq/my-first-repo.git`
es la URL del repositorio remoto. Debería, por supuesto, sustituir `mamaciasq`
por su nombre de usuario de GitHub para que se corresponda con su URL de repositorio remoto.
Más adelante explicaremos por qué "origen" es el nombre que elegimos para este control remoto.
Vamos a ejecutar `git remote` nuevamente para confirmar que agregamos el control remoto` origin`
exitosamente:

```{r, engine='bash', eval=FALSE}
git remote
```

```
## origin
```

Ahora que hemos agregado nuestro control remoto GitHub, realicemos nuestra primer subida **push** de Git. Un
Git push actualiza un repositorio remoto con todos los commits que hemos realizado en
nuestro repositorio local de Git. Esta primer subida que hace al configurar un control remoto
en GitHub con un repositorio local es un poco diferente de las futuras subidas de Git.
Tendremos que usar la bandera `-u` para establecer `origen` como el predeterminado
repositorio así que no tendremos que proporcionar su nombre cada vez que queramos interactuar
con eso. Ingrese el siguiente comando modificado para que esté usando su
nombre de usuario de GitHub:

```{r, engine='bash', eval=FALSE}
git push -u origin master
```

```
## Counting objects: 23, done.
## Delta compression using up to 4 threads.
## Compressing objects: 100% (19/19), done.
## Writing objects: 100% (23/23), 1.88 KiB | 0 bytes/s, done.
## Total 23 (delta 9), reused 0 (delta 0)
## remote: Resolving deltas: 100% (9/9), done.
## To https://github.com/seankross/my-first-repo.git
##  * [new branch]      master -> master
## Branch master set up to track remote branch master from origin.
```

El comando anterior subió todas nuestras confirmaciones al repositorio remoto en
GitHub, y configuró la rama `master` del repositorio remoto `origin` como
el repositorio remoto predeterminado. 

Una buena característica de GitHub es que los archivos README se representan en la página del repositorio para que pueda escribir documentos que explican el contenido de su repositorio.
Vamos a ser más creativos con estos documentos Readme aprendiendo un pequeño
lenguaje llamado Markdown.

### Markdown

Markdown es un lenguaje de marcado. Los lenguajes de marcado son conjuntos de reglas para agregar características decorativas para enviar mensajes de texto. El lenguaje de marcado más popular es HTML, pero también podría haber oído hablar de XML y LaTeX.
Markdown es un poderoso lenguaje de marcado porque es
pequeño, intuitivo y legible cuando está escrito como texto sin formato. GitHub
transforma los archivos de Markdown (que terminan en la extensión de archivo `.md`) en simples
páginas web HTML en su repositorio. Si hay un archivo llamado `README.md` en cualquier
carpeta en su repositorio, ese archivo se procesa en HTML y se muestra en
GitHub. Vamos a crear un archivo `README.md` para nuestro repositorio. Primero destruiremos
el archivo Readme de texto sin formato que ya tenemos:


```{r, engine='bash', eval=FALSE}
rm readme.txt
```

Hemos incluido un archivo de Markdown a continuación que intenta explicar algunas
caracteristicas de Markdown. Copie el texto sin formato, a continuación, cree un nuevo archivo llamado `README.md` con
`nano`, pegue el texto y luego guarde el archivo.

    # This is a large heading

    ## This is a smaller heading

    And as **imagination** bodies forth,
    The forms of things *unknown*, the poet’s pen,
    Turns them to shapes and gives to airy nothing,
    A local *habitation* and a **name**.

    - This is
    - an unordered
    - list

    1. This is
    2. an ordered
    3. list

    Here is `some code` in the middle of a sentence.

    ```
    This is
    a block
    of code
    ```

    Here is how you make [a link](https://www.wikipedia.org/).

    ![This is an image.](https://github.com/yihui/xaringan/releases/download/v0.0.2/karl-moustache.jpg)

```{r, engine='bash', eval=FALSE}
nano README.md
```

Ahora agreguemos nuestros cambios, realicemos una confirmación e impulsemos esos cambios en nuestro repositorio remoto:

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "added README.md"
git push
```

```
## Counting objects: 3, done.
## Delta compression using up to 4 threads.
## Compressing objects: 100% (3/3), done.
## Writing objects: 100% (3/3), 659 bytes | 0 bytes/s, done.
## Total 3 (delta 0), reused 0 (delta 0)
## To https://github.com/seankross/my-first-repo.git
##    ca04f67..2169912  master -> master
```

Como ya configuramos un repositorio remoto predeterminado la primera vez que subimos archivos, podemos
ahora simplemente ingresar `git push` para enviar nuestras últimas confirmaciones a la rama `master` en el remoto 'origin'. 

¡Tenemos un archivo readme mucho más complejo! Observe cómo el texto simple que nosotros
escribimos se ha procesado de acuerdo con algunas reglas:

- Los signos de número (`#`, `##`) crean encabezados.
- Una palabra rodeada de asteriscos únicos (`*palabra*`) hace que la palabra esté *en cursiva*.
- Una palabra rodeada de dos asteriscos (`**palabra**`) hace que la palabra **sea negrita**.
- Puede crear listas con guiones (`-`) o números (` 1., 2., 3.`).
- El código se puede colocar en el medio de una línea con solo comillas simples (`` `codigo` ``).
- Se puede crear un bloque de código colocando el código entre un conjunto de triples
comillas simples (`` ``` ``).
- Puede insertar un enlace con corchetes y paréntesis (`[Enlace de texto aquí](http://jhu.edu)`).
- Puede usar una imagen con un signo de exclamación y un enlace a una imagen (`![Texto alternativo aquí](http://jhu.edu/jeff.jpg)`)

Se sugiere que se tome unos minutos para jugar con la sintaxis [de este editor de Markdown en línea](https://jbt.github.io/markdown-editor/#TVFLbtwwDN3rFCxm0xgTOU133WXXA2QXFDDHYizWEmlIctzZ9Rq9Xk9SetqZFNCCIt97/LwDPEeuYA8hYZkIImFgmZw7HP6r1YwpUXmvPkkArNB1nHFiwcYqXQcnDUwVXrW0eHTPkfYwV9BXaNGIxlhlFt2kO1qGYFFqv3/+qrCQGGEtUvd8hqZQIy4mhtZq4jeLLIdcziB6ETu6J0g6YoIu4onb3yEueLTJBDN1nXfu/rqIRSiwipZAhYJ9E9fm3Cd/Qzz6HXIFfPb/EF/tu19iqJoJRg00AMtlg8whJNo3tDORNJKRrOkwDO4qinCyOWdnmJ16qd0ko25w1hUyzgQvZgPL/O1jbG2pX/p+2za/8cwLBUavZervTPzDy80agd0B8u+UiVtcT37U3J85rtz/wGLXQukLJcJKtQ9mQFIM/duDf/CP/Ywl3Wdda8Mxkv++THd/AA==).
Para más información sobre Markdown, vea la ayuda de GitHub
[*Mastering Markdown*](https://guides.github.com/features/mastering-markdown/)
guía.

### Pull Requests

Las siguientes dos características de GitHub que vamos a discutir: **pull request** y
**forking** - son lo que hace que GitHub sea tan genial. Un pull request le permite
comparar de forma interactiva dos ramas diferentes antes de fusionarlas para que pueda
ya sea continuar con la fusión o proporcionar comentarios a quien abrió el pull request. Esencialmente, un pull request permite que una persona pregunte a otra persona si
están dispuestos a incorporar cambios en una rama en otra rama. Esta
transacción puede involucrarlo a usted y a un colaborador, usted y un
extraño, o puede abrir un pull request en su propio repositorio como
método de mantenerse organizado.

Como no puedo garantizarle que tenga un colaborador, le mostraré cómo abrir
un pull request en su propio repositorio. Primero en su repositorio local `my-first-repo` 
cambiemos a la rama `update-readme`.

```{r, engine='bash', eval=FALSE}
git checkout update-readme
```

```
## Switched to branch 'update-readme'
```

Echemos un vistazo a lo que está actualmente en esta rama:

```{r, engine='bash', eval=FALSE}
ls
```

```
## bernie.jpg
## toby.jpg
## file1.txt
## file2.txt
## readme.txt
```

Parece que no hemos actualizado esta rama para estar al día con la rama `master`. Podemos hacer esto fácilmente al fusionarnos en la rama `master`.

```{r, engine='bash', eval=FALSE}
git merge master
```

```
## Updating 5aa94fa..2169912
## Fast-forward
##  README.md  | 28 ++++++++++++++++++++++++++++
##  readme.txt |  4 ----
##  2 files changed, 28 insertions(+), 4 deletions(-)
##  create mode 100644 README.md
##  delete mode 100644 readme.txt
```

Ahora las ramas `master` y `update-readme` son idénticas. Vamos a limpiar este
directorio para que pueda hacer un pequeño proyecto de Markdown personalizado. primero
borremos todos los archivos en este directorio que realmente no necesitamos,
es decir todo excepto `README.md`.

```{r, engine='bash', eval=FALSE}
rm *.txt
rm *.jpg
ls
```

```
## README.md
```

Ahora que hemos limpiado nuestro repositorio, abrimos `README.md` con `nano`.
Borre todo lo que está escrito allí y escriba algunas líneas sobre usted mismo.
En el bloque de texto a continuación, puede ver lo que se ha escrito en `README.md`.

```
# Sean Kross

### Geography

I live in the city of Baltimore, in the state of Maryland, in the United States
of America.

### Reading

Three of my favorite books are:

- *Mindstorms* by Seymour Papert
- *Welcome to the Monkey House* by Kurt Vonnegut
- *Persepolis* by Marjane Satrapi

### Food

Last night I dreamt about eating in these restaurants:

1. Linger in Denver.
2. Azura in Jerusalem.
3. Gemma in New York City.

### Contact

The best way to get in touch with me is [on Twitter](https://twitter.com/seankross).
```

Una vez que haya escrito algunas cosas divertidas sobre usted, agregue sus cambios y
haga un nuevo commit.

```{r, engine='bash', eval=FALSE}
git add -A
git commit -m "made readme more personal"
```

Al igual que un repositorio local de Git, los repositorios remotos en GitHub pueden tener múltiples
ramas. Llevemos esta confirmación a la rama `update-readme` en GitHub mediante un push:

```{r, engine='bash', eval=FALSE}
git push origin update-readme
```

```
## Counting objects: 3, done.
## Delta compression using up to 4 threads.
## Compressing objects: 100% (3/3), done.
## Writing objects: 100% (3/3), 630 bytes | 0 bytes/s, done.
## Total 3 (delta 0), reused 0 (delta 0)
## To https://github.com/seankross/my-first-repo.git
##  * [new branch]      update-readme -> update-readme
```

Tenga en cuenta que necesitábamos especificar a qué control remoto estábamos subiendo puesto que GitHub
no sabe previamente sobre la existencia de la rama `update-readme`.
Cuando realiza un `git push`, solo se envían las confirmaciones en la rama actual
al repositorio remoto. De esta forma puede crear branches locales a los que no pueden ser
accedidos desde el repositorio remoto, a menos que los suba explícitamente en GitHub.

Ahora volvamos a la página de GitHub de nuestro repositorio. En el lado izquierdo de la
página debería ver un botón que dice "Branch: master". Haga clic en ese botón
y debería aparecer un pequeño menú desplegable.

Haga clic en "update-readme" en el menú para ver los archivos en esa rama. ¡Usted
debería ver que los archivos `README.md` son diferentes! Puede intercambiar entre ramas usando este menú.

Ahora que ha enviado una rama actualizada a GitHub, vamos a abrir un pull request.
Un pull request es como un 'git merge' guiado que es facilitado por GitHub. Para
iniciar el pull request haga clic en el botón "New pull request" al lado del
botón del branch. 

Hay algunos detalles importantes en esta página, así que revisémoslos. Primero
bajo el encabezado "Open a pull request", puede ver los nombres de dos ramas.
El nombre de la rama después de "base:" muestra la rama en la que los cambios se están fusionando (en este caso, la rama `master`), y el nombre de la rama después de "compare"
muestra la rama que tiene los cambios (en este caso, la rama `update-readme`).

En los cuadros de texto a continuación puede escribir un título para su pull request (el 
título predeterminado en este caso es el nombre del último commit) y puede escribir comentarios
sobre el pull request que puede formatear con Markdown. Si está
colaborando con alguien más en un proyecto, es importante escribir buenos
comentarios para que sus colaboradores sepan qué cambios ha realizado en la rama
que está solicitando fusionar. Si se desplaza hacia abajo en
la página puede ver una comparación línea por línea de los cambios en la rama "compare"
comparada con la rama "base". Cuando haya terminado de revisar estos
cambios haga clic en el botón verde "Create pull request" para abrir  el pull request. 

¡Felicitaciones por abrir su primer pull request! Echemos un vistazo a lo que está
sucediendo en esta página. Debajo del título del pull request podemos ver tres
pestañas llamadas **Conversation**, **Commits** y **Files changed**. En la
pestaña **Conversation** podemos agregar comentarios al pull request que puede ser
formateado con Markdown. La pestaña **Commits** enumera los commits que han sido
hechos a la rama "compare" en estpull request. Finalmente la pestaña **Files changed**
muestra la misma comparación línea por línea que vimos antes.

Por lo general, cuando trabaja con colaboradores, hay una gran cantidad de
discusión que ocurre después de abrir un pull request. Git confirma que son
subidos a la rama "compare" (`update-readme` en este caso) del repositorio de GitHub
se reflejará en un pull request incluso después de que la solicitud haya sido
abierta. De esta manera, los cambios que se realizan como resultado de la discusión pueden ser
fácilmente incorporados. Una vez que esté listo, regrese a la pestaña **Conversation** y haga clic en
el botón verde "Merge pull request", luego haga clic en el botón verde "Confirm merge"
que aparece. Esto hará `git merge` en la rama de "compare" con la rama "base" en nuestro repositorio remoto. ¡Acaba de fusionar su primer pull request! Ahora
haga clic cerca de la esquina superior izquierda de esta página en la pestaña **<>Code**, y 
debería ver que los cambios de la rama `update-readme` se han fusionado
en `master`.

Cuando trabaja en un repositorio remoto de GitHub con muchas otras personas, estos pull requests y los fusiones pueden suceder sin que usted se involucre en absoluto, si las confirmaciones afectan partes del código en las que no está trabajando. Aún así es importante
mantener su repositorio local actualizado con los últimos cambios en el repositorio remoto. Volvamos a su terminal donde tiene el repositorio `my-first-repo`
como el directorio de trabajo actual.

Primero cambiemos a la rama `master`.

```{r, engine='bash', eval=FALSE}
git checkout master
```

Ahora actualicemos nuestra rama principal local con los commits que se han fusionado
en la rama principal en nuestro repositorio remoto. Podemos lograr esto con
el comando `git pull`:

```{r, engine='bash', eval=FALSE}
git pull
```

```
## remote: Counting objects: 1, done.
## remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
## Unpacking objects: 100% (1/1), done.
## From https://github.com/seankross/my-first-repo
##    2169912..b9217f6  master     -> origin/master
## Updating 2169912..b9217f6
## Fast-forward
##  README.md | 38 ++++++++++++++++++--------------------
##  file1.txt |  0
##  file2.txt |  0
##  3 files changed, 18 insertions(+), 20 deletions(-)
##  delete mode 100644 file1.txt
##  delete mode 100644 file2.txt
```

Con `git pull` Git encuentra la rama `master` en el repositorio remoto `origin`
y actualiza nuestro repositorio local con los nuevos commits. ¡Ya ha completado el
ciclo de vida de un pull request completo! En la sección **Forking**,
se vuelve a discutir cómo GitHub supercarga los pull requests para
fomentar una mayor comunidad de codificación.


### Pages

Por ahora vamos a tomar un pequeño desvío para discutir
[GitHub Pages](https://pages.github.com/). GitHub Pages le permite crear
y alojar un sitio web en GitHub usando solo Git y Markdown. Regrese a su
página del repositorio `my-first-repo` en GitHub al hacer clic en la pestaña *Settings* en la
parte superior. Desplácese hacia abajo en la página hasta que vea un cuadro que dice **GitHub Pages**. Entonces
haga clic en el menú desplegable que dice **None**. 

Haga click en la rama *master* y luego haga click en *Save*. Ahora vaya al website
[your-github-username].github.io/my-first-repo (en este caso la dirección es
[mamaciasq.github.io/my-first-repo](http://mamaciasq.github.io/my-first-repo))
y debería ver su propio website!

¿¡Cuan genial es eso!? Si desea cambiar su nuevo sitio web, todo lo que necesita hacer
es editar su `README.md` luego confirmar y subir los cambios! Sitios web como estos
son excelentes para mostrar proyectos, proporcionar documentación de software, crear
currículos en línea, o escribir un blog! Los sitios web de las páginas de GitHub pueden ser tan simples como
pocos documentos Markdown, o si conoce alguna programación web, puede volverlos
sitios web complejos. Para obtener más información acerca de las páginas de GitHub, puede
echar un vistazo a la [documentación aquí](https://pages.github.com/).

### Forking

Si está leyendo este gist, es bastante seguro decir que probablemente interactúa
con software todos los días. El software alimenta su computadora, Internet, su
teléfono y este gist. Considerando todo el software que usa, ¿alguna vez
ha pensado en modificar ese software? Tal vez podría escribir algún código para agregar
una nueva característica que cree que sería útil o para solucionar un error que haya notado.
GitHub facilita la modificación del software de otras personas a través del proceso de
**forking**. Bifurcar un repositorio de GitHub, copia el repositorio GitHub de otra persona
en su cuenta de GitHub. A continuación, puede modificar esta copia de su
software como quiera. Después de agregar algunas confirmaciones a su copia del
repositorio, puede guardar los nuevos commits para usted, compartirlos con
otros, o puede abrir un **pull request** para fusionar sus nuevos commits
en el repositorio fuente original. Este repositorio fuente original (el
repositorio que ha bifurcado) a menudo se denomina repositorio *upstream*.

Tratemos de crear un repositorio ahora. Vaya
https://github.com/seankross/the-unix-workbench y haga clic en el botón **Fork**
en la esquina superior derecha. GitHub luego le preguntará qué cuenta desea
usar para bifurcar el repositorio. Si es un nuevo usuario de GitHub, solo tiene una
cuenta, así que seleccione esa cuenta. Después de una breve pantalla de "por favor espere", debería
luego ver el repositorio bifurcado en la URL
https://github.com/[your-github-username]/the-unix-workbench. Ahora ha bifurcado
un repositorio! Para obtener una copia local del repositorio, necesitará usar el comando `git clone`.

La clonación de un repositorio copia un repositorio de Git en su computadora mientras mantiene
seguimiento del repositorio remoto del que se originó. Vamos a clonar su bifurcación 
del repositorio recién añadido ahora. En el lado derecho de la página del repositorio debería ver
un botón verde que dice **Clone or download**. 

Haga clic en el pequeño icono del portapapeles que copiará la URL de Git. Ahora vuelva a
la terminal y cambie su directorio de trabajo a su directorio de inicio.


```{r, engine='bash', eval=FALSE}
cd
pwd
```

```
## /Users/sean
```

Ahora clonémos el repositorio. Escriba `git clone` en la terminal y luego
pegue en la URL de Git lo que copiamos de GitHub:

```{r, engine='bash', eval=FALSE}
git clone https://github.com/[your-github-username]/the-unix-workbench.git
```

```
## Cloning into 'the-unix-workbench'...
## remote: Counting objects: 669, done.
## remote: Compressing objects: 100% (7/7), done.
## remote: Total 669 (delta 2), reused 8 (delta 2), pack-reused 660
## Receiving objects: 100% (669/669), 4.00 MiB | 4.55 MiB/s, done.
## Resolving deltas: 100% (510/510), done.
```

Ahora `cd` en su repositorio clonado.

```{r, engine='bash', eval=FALSE}
cd the-unix-workbench
```

¡Acaba de completar con éxito su primer clon de Git! Como mencionamos
antes, la clonación tiene la ventaja de hacer un seguimiento del repositorio remoto que
debería estar asociado con el repositorio local. Probemos esto ingresando
`git remote` con la etiqueta `-v`:

```{r, engine='bash', eval=FALSE}
git remote -v
```

```
## origin	https://github.com/[your-github-username]/the-unix-workbench.git (fetch)
## origin	https://github.com/[your-github-username]/the-unix-workbench.git (push)
```

Como puede ver el nombre predeterminado del repositorio remoto después de clonar el
repositorio es `origin`. Ahora que ha clonado su repositorio bifurcado, debe agregar un
¡commit! Un cambio que sugiero es agregar su nombre a `guestbook.md`. Vamos a
hacer esto ahora:

```{r, engine='bash', eval=FALSE}
echo "- Sean Kross" >> guestbook.md # ¡Obviamente agregue su nombre!
cat guestbook.md
```

```
## # Guest Book
##
## - Sean Kross
```

Ahora agreque, confirme, y suba sus cambios:

```{r, engine='bash', eval=FALSE}
git add guestbook.md
git commit -m "added my name to guestbook.md"
git push
```

Ahora que ha agregado su nombre al libro de visitas, puede fusionar su cambio en
la versión del libro de visitas abriendo un nuevo pull request como se describe en
la sección anterior. Si su pull request se fusiona al libro de visitas en el
repositorio, entonces habrá completado el ¡ciclo vital! de GitHub completo.


El proceso de bifurcar un repositorio, hacer cambios y luego abrir un pull
request es un flujo de trabajo muy potente para ver los cambios que desea hacer en
el mundo del software. Muchos proyectos de software grandes e importantes tienen repositorios
en GitHub incluyendo [sistemas operativos](https://github.com/torvalds/linux),
[lenguajes de programación](https://github.com/golang/go),
e incluso [Git en sí mismo](https://github.com/git/git)! Si hay un cambio que quiera
para ver en un repositorio público de GitHub, bifurcar ese repositorio y hacer el cambio es la opción!

### Resumen

- Puede usar GitHub para crear y alojar repositorios remotos de Git.
- Un repositorio remoto de Git es un repositorio de Git que siempre está conectado a
Internet.
- Liste los repositorios remotos con `git remote`.
- Agregue repositorios remotos con `git remote add [nombre-de-remoto] https://github.com/[username]/[repo-name].git`
- Agregue commits a su repositorio remoto con `git push [nombre-de-remoto][nombre-de-rama]`
o simplemente `git push` si ha configurado un control remoto y una bifurcación predeterminados.
- Para fusionar confirmaciones en un repositorio remoto en el uso de su repositorio local
`git pull [nombre-de-control remoto] [nombre-de-rama]` o simplemente `git pull` si ha configurado un control remoto y un branch predeterminados.
- Un pull request le permite comparar interactivamente dos ramas diferentes
antes de fusionarlas.
- ¡GitHub Pages le permite alojar sitios web escritos en Markdown gratis!
- Bifurcar un repositorio le permite hacer cambios a una copia de un repositorio público. A continuación, puede abrir un pull request si cree que sus cambios deberían
¡fusionarse en el repositorio upstream!

### Ejercicios

1. Cree un nuevo repositorio en GitHub. Clone su repositorio y agregue un
`README.md` archivo. Suba este archivo a GitHub y cree un sitio web de GitHub Pages
para este repositorio.
2. Bifurque un repositorio existente (pruebe uno de los de https://github.com/seankross)
e intente identificar algo valioso que podría contribuir. Haga cambios o
adiciones a ese repositorio, luego abra un pull request.
3. Lea las [Guías de GitHub](https://guides.github.com/).
