# Introduccion GITHUB  

### Crear un directorio:
	 mkdir prueba_git
### Acceder a ese directorio : 
	cd prueba_git

### Crear mediante un editor de texto dos archivos: 
	nano texto.txt (Ctrl + o para guardar, Ctrl + x para salir)
	nano script.sh
## 1. Inicialización

### Añadirlo como nuevo repositorio local:
	git init (ahora mismo git no los tiene en cuenta para ser parte del repositorio, ya que estan sin rastreo (untracked))
	 git init
Initialized empty Git repository in C:/Users/lugon/OneDrive/Escritorio/prueba_gi
t/.git/

### Ahora mismo tenemos un repositorio git con dos archivos sin rastreo (untracked) , lo comprobamos ejecutando git status:
	 git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)


### Cambiar el nombre de la rama principal:
	git branch -m main

### volver a restaurarlo a master:
	git branch -m master
## 2. Añadiendo archivos

### Añadir el archivo script.sh a archivos rastreados:
	git add script.sh
	git status ( para comprobar que efectivamente el estado cambia a TRACKED)
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   script.sh

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt


### Para confirmar que si hay cambios se sincronizaran con los equipos remotos:
	git commit -m "Confirmacion inicial" (mensaje opcional)
[master (root-commit) 186e768] Confirmacion inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh

### Si ahora ejecutamos git status vemos que solo texto.txt no esta en seguimiento:
	On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)


### Con cada commit es habitual poner un mensaje, si fuera muy largo se haria asi:
	git commit -F mensaje.txt

### Añadimos a texto.txt:
	git add texto.txt
	git commit -m “Añadido archivo texto.txt”
[master 314711a] Añadido archivo texto.txt
 1 file changed, 3 insertions(+)
 create mode 100644 texto.txt
	git status
On branch master
nothing to commit, working tree clean

## 3.Modifcando archivos

### Modificar el archivo texto.txt:
	nano texto.txt
	git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")

	git add texto.txt
	git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

### Si ahora volvemos a modificar el texto.txt y ejecutamos git status:

On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt


### Hacer un add para incluir la ultima modificacion:
	git add texto.txt
	git commit -m “Ampliada la explicación del texto”
	git status
On branch master
nothing to commit, working tree clean

## 4. Informacion 

### Se puede resumir un paso entre los add y los commits:
	git commit -a -m “Nueva versión” (si hay un nuevo archivo es necesario hacer add)

### Para ver la informacion de la ultima version confirmada:
	git show
commit d8e1c4726e6acd11ee2081845ec243861e73e052 (HEAD -> master)
Author: lugonpa10 <lugonpa10@gmail.com>
Date:   Sat Oct 25 10:28:45 2025 +0200

    Ampliada la explicacion del texto

diff --git a/texto.txt b/texto.txt
index 15bf608..23c83ff 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,3 +1,5 @@
 uno
 dos
 tres
+cuatro
+cinco


### Para ver los cambios historicos:
	git log

commit d8e1c4726e6acd11ee2081845ec243861e73e052 (HEAD -> master)
Author: lugonpa10 <lugonpa10@gmail.com>
Date:   Sat Oct 25 10:28:45 2025 +0200

    Ampliada la explicacion del texto

commit 314711a8f3ee26423ea7c4871386145219902a2b
Author: lugonpa10 <lugonpa10@gmail.com>
Date:   Sat Oct 25 10:21:14 2025 +0200

    Añadido archivo texto.txt

commit 186e7684f653f1cc0c5f431d54f2f3eced2fcbb9
Author: lugonpa10 <lugonpa10@gmail.com>
Date:   Sat Oct 25 10:17:43 2025 +0200

    Confirmacion inicial




### Diferencias entre un archivo modificado y el que se ha confirmado en la ultima version:
	git diff
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git to
uches it
diff --git a/texto.txt b/texto.txt
index 23c83ff..b7298b3 100644
--- a/texto.txt (archivo previo)
+++ b/texto.txt (archivo final)
@@ -1,5 +1,6 @@
 uno
 dos
-tres
+
 cuatro
 cinco
+seis

### Para ver informacion entre lo añadido y lo eliminado:
	git commit -a -m "Probando diff" (filas cambiadas,elementos añadidos y elminados)
[master 5f8c0f6] Probando diff
 1 file changed, 2 insertions(+), 1 deletion(-)

### Añadimos la palabra siete al archivo texto.txt y probamos git diff:

diff --git a/texto.txt b/texto.txt
index b7298b3..430cdae 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,6 +1,6 @@
 uno
 dos
-
 cuatro
 cinco
 seis
+siete


### Para ignorar ciertos archivos que no nos interesa gestionar, como los .class en java creamos este archivo:nano .gitignore y contiene las siguientes lineas:

 ignora los archivos terminados en .class
*.class
 ignora los archivos terminados en ~
*~
 pero no importante~, aun cuando había ignorado los archivos
terminados en ~ en la linea anterior
!importante~
(los # es el equivalente a // en java)

### Luego creamos el archivo Hola.java:
	nano Hola.java que contiene:
	class Hola {
 public static void main(String[] args){
 System.out.println("Welcome to the Java World");
 }
}

### Y tambien los siguientes archivos vacios:
	nano temporal~
	nano importante~

### Para listarlos el comando:
	ls -a
./  ../  .git/  .gitignore  Hola.java  importante~  script.sh  temporal~  texto.txt

### Ejecutamos el Hola.java para que al listarlo aparezca Hola.class:
	javac Hola.java

### Si ejecutamos git status ahora nos sale:
	On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        Hola.java
        importante~

no changes added to commit (use "git add" and/or "git commit -a")

### Ponemos el siguiente comando:
	git add . (con el punto indicamos que añada todo lo que esta pendiente)
	git commit -m “Añadidos fuentes en java y archivos importantes”
[master a106fd4] Añadidos fuentes en java y archivos importantes
 4 files changed, 13 insertions(+), 1 deletion(-)
 create mode 100644 .gitignore
 create mode 100644 Hola.java
 create mode 100644 importante~



### Para ver los archivos que hay en el directorio tras el ultimo commit:
	git ls-tree --name-only -r HEAD

	.gitignore
	Hola.java
	importante~
	script.sh
	texto.txt

### El comando git log sirve para ver el historial de versiones,aparece un codigo al lado de la palabra commit:
	commit d8e1c4726e6acd11ee2081845ec243861e73e052

### Para referenciar este numero es bastante complicado, por ejemplo con git show nos muestra informacion sobre el commit y la comparacion de dicha version con la previa:
	git show d8e1c4726e6acd11ee2081845ec243861e73e052
commit d8e1c4726e6acd11ee2081845ec243861e73e052
Author: lugonpa10 <lugonpa10@gmail.com>
Date:   Sat Oct 25 10:28:45 2025 +0200

    Ampliada la explicacion del texto

diff --git a/texto.txt b/texto.txt
index 15bf608..23c83ff 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,3 +1,5 @@
 uno
 dos
 tres
+cuatro
+cinco





### Referenciar estos numeros es más fácil con tags,para añadir uno a la version actual:
	 git tag v0.7

### Para añadirla a una version anterior se añade el código hash al final del comando:
	git tag v0.3 d8e1c4726e6acd11ee2081845ec243861e73e052

### Para ver de forma abreviada las versiones y los tags:
	git log --oneline
a106fd4 (HEAD -> master, tag: v0.7) Añadidos fuentes en java y archivos importantes
5f8c0f6 Probando diff
d8e1c47 (tag: v0.3) Ampliada la explicacion del texto
314711a Añadido archivo texto.txt
186e768 Confirmacion inicial



### Para ver una version determinada:
	git show v0.3
commit d8e1c4726e6acd11ee2081845ec243861e73e052 (tag: v0.3)
Author: lugonpa10 <lugonpa10@gmail.com>
Date:   Sat Oct 25 10:28:45 2025 +0200

    Ampliada la explicacion del texto

diff --git a/texto.txt b/texto.txt
index 15bf608..23c83ff 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,3 +1,5 @@
 uno
 dos
 tres
+cuatro
+cinco


### Para ir a una version antigua del proyecto:
	git checkout v0.3

### Y luego volver a la mas reciente (si en vez de master has puesto main,en el comando hay que poner este ultimo):
	git checkout master
Previous HEAD position was d8e1c47 Ampliada la explicacion del texto
Switched to branch 'master'


### Crear una rama:
	git branch Prueba
	
### Y si ejecutamos:
	git log --oneline

a106fd4 (HEAD -> master, tag: v0.7, Prueba) Añadidos fuentes en java y archivos importantes
5f8c0f6 Probando diff
d8e1c47 (tag: v0.3) Ampliada la explicacion del texto
314711a Añadido archivo texto.txt
186e768 Confirmacion inicial


### Aparecen dos ramas en la version mas reciente (master y Prueba),si hay mas cambios y commits los hacemos en master porque es donde apunta HEAD

### Si ejecutamos git branch nos sale el listado de ramas y marcada con un asterisco en la que estamos actualmente:
	  Prueba
	* master

### Cambiar de rama:
	git switch Prueba o git checkout Prueba
lugon@DESKTOP-MAHL92I MINGW64 ~/OneDrive/Escritorio/prueba_git (Prueba)

Switched to branch 'Prueba'


### Ahora el prompt ya muestra la nueva rama y si ejecutamos git branch de nuevo:
	* Prueba
 	 master

### Aparece el asterisco ya en Prueba (rama actual)

### Ejecutamos git log --oneline:

a106fd4 (HEAD -> Prueba, tag: v0.7, master) Añadidos fuentes en java y archivos importantes
5f8c0f6 Probando diff
d8e1c47 (tag: v0.3) Ampliada la explicacion del texto
314711a Añadido archivo texto.txt
186e768 Confirmacion inicial


### HEAD ya apunta a prueba porque es nuestra rama actual y por lo tanto cualquier commit que hagamos no afectara a la rama principal.

### Cambiar el archivo Hola.java:
	System.out.println("I have no more branches to commit, said the Ent");

### Guardamos los cambios y especifiamos la version:
	git commit -a -m “Llegan los Ents a Java”
	git tag v0.7-Ent-Release

### Lo comprobamos ejecutando git log --oneline:

7b16a1d (HEAD -> Prueba, tag: v0.7-Ent-Release) LLegan los Ents a Java
a106fd4 (tag: v0.7, master) Añadidos fuentes en java y archivos importantes
5f8c0f6 Probando diff
d8e1c47 (tag: v0.3) Ampliada la explicacion del texto
314711a Añadido archivo texto.txt
186e768 Confirmacion inicial


### Cambiamos de rama y comprobamos que la version previa sigue ahí:
	git switch master
	cat Hola.java
class Hola{
public static void main(String[] args){
System.out.println("Welcome to the Java World");
        }
}

### Si queremos juntar el experimento con nuestra rama Principal (muchas veces este paso da conflictos):
	git merge Prueba
Updating a106fd4..7b16a1d
Fast-forward
 Hola.java | 1 +
 1 file changed, 1 insertion(+)

### Eliminar archivos:
	git rm importante
	git commit -m "Eliminar importante~"
[master 06268f3] Eliminar importante
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 importante~


### Si quieres quitar algun archivo ya en seguimiento (los .class por ejemplo):
	git reset HEAD *.class

### Clonar un repositorio:
	git clone URL del repositorio

### Mandar cambios al repositorio remoto:
	git push -u origin master

### Despues de la primera vez simplemente se ejecuta:
	git push

### Si queremos sincronizar un repositorio local que ya estas usando con uno remoto:
	git remore add origin URL del repositorio
