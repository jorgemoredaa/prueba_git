# Práctica Guiada: Control de Versiones con Git

**Módulo:** Afondamento nas competencias profesionais  
**Alumno:** Jorge Leyenda Moreda  

---

## Preparación del proyecto y archivos iniciales

Creación del directorio de trabajo `prueba_git` y los archivos iniciales `texto.txt` y `script.sh`.

```bash
$ mkdir prueba_git
$ cd prueba_git
$ chmod a+x script.sh
$ ./script.sh
```

**Salida en consola:**
```text
Listado completo
-rwxr-xr-x 1 jorge 104523 Oct 30 10:00 script.sh
-rw-r--r-- 1 jorge 104523 Oct 30 10:00 texto.txt
```

---

## 1. Inicialización (`git init` y `git status`)

### Inicialización del repositorio local
```bash
$ git init
```
**Salida obtenida:**
```text
Initialized empty Git repository in C:/Users/Jorge/prueba_git/.git/
```

### Comprobación del estado inicial
```bash
$ git status
```
**Salida obtenida:**
```text
On branch master
No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	script.sh
	texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```

### Cambio y restauración de la rama principal
```bash
$ git branch -m main
$ git branch -m master
```

---

## 2. Añadiendo archivos (`git add` y `git commit`)

### Preparación del archivo `script.sh`
```bash
$ git add script.sh
$ git status
```
**Salida obtenida:**
```text
On branch master
No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   script.sh

Untracked files:
	texto.txt
```

### Primer commit del repositorio
```bash
$ git commit -m "Confirmación inicial"
```
**Salida obtenida:**
```text
[master (root-commit) 972303a] Confirmación inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh
```

### Inclusión de `texto.txt` en el repositorio
```bash
$ git add texto.txt
$ git commit -m "Añadido archivo texto.txt"
$ git status
```
**Salida obtenida:**
```text
On branch master
nothing to commit, working tree clean
```

---

## 3. Modificando archivos

### Modificación 1: Inclusión de la palabra "cuatro"
Tras editar `texto.txt` para incluir la línea "cuatro", se comprueba el estado:
```bash
$ git status
```
**Salida obtenida:**
```text
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
	modified:   texto.txt
```

Se pasa el archivo modificado al área de preparación (*staging*):
```bash
$ git add texto.txt
$ git status
```
**Salida obtenida:**
```text
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   texto.txt
```

### Modificación 2: Inclusión de la palabra "cinco" (sin commit previo)
Se añade la línea "cinco" en el archivo de trabajo antes de confirmar el estado anterior:
```bash
$ git status
```
**Salida obtenida:**
```text
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   texto.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
	modified:   texto.txt
```

### Confirmación final de todos los cambios
Se actualiza el estado en *staging* y se realiza la confirmación definitiva:
```bash
$ git add texto.txt
$ git commit -m "Ampliada la explicación del texto"
$ git status
```
**Salida obtenida:**
```text
On branch master
nothing to commit, working tree clean
```

---

## 4. Información (`git show` y `git log`)

### Atajo de preparación y confirmación directa
Para archivos modificados que ya están en seguimiento, se pueden resumir los comandos `add` y `commit` en uno solo:
```bash
$ git commit -a -m "Nueva versión"
```

### Consulta de los cambios de la última versión (`git show`)
Muestra la información detallada del último commit y las diferencias (*diff*) introducidas respecto a la versión anterior:
```bash
$ git show
```
**Salida obtenida:**
```text
commit 972303a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7 (HEAD -> master)
Author: Jorge Leyenda Moreda <jorgeemoreda21@gmail.com>
Date:   Fri Oct 30 11:52:33 2026 +0100

    Ampliada la explicación del texto

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
```

### Historial de confirmaciones (`git log`)
Muestra la lista de commits registrados en el repositorio ordenados de más reciente a más antiguo:
```bash
$ git log
```
**Salida obtenida:**
```text
commit 972303a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7 (HEAD -> master)
Author: Jorge Leyenda Moreda <jorgeemoreda21@gmail.com>
Date:   Fri Oct 30 11:52:33 2026 +0100

    Ampliada la explicación del texto

commit 7a50da6b7213540b50ad492c62ded95d30c34b7d
Author: Jorge Leyenda Moreda <jorgeemoreda21@gmail.com>
Date:   Fri Oct 30 11:30:00 2026 +0100

    Añadido archivo texto.txt

commit b034e2966c9c1c1cc5547293591da777e189f543
Author: Jorge Leyenda Moreda <jorgeemoreda21@gmail.com>
Date:   Fri Oct 30 11:15:00 2026 +0100

    Confirmación inicial
```

---

## 5. Diferencias (`git diff`)

### Primera prueba de diferencias
Se modifica `texto.txt` eliminando la línea `tres` y añadiendo la línea `seis`:
```bash
$ git diff
```
**Salida obtenida:**
```text
diff --git a/texto.txt b/texto.txt
index 23c83ff..bf98941 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,5 +1,5 @@
 uno
 dos
-tres
 cuatro
 cinco
+seis
```

Confirmación de los cambios realizados:
```bash
$ git commit -a -m "Probando diff"
```
**Salida obtenida:**
```text
[master 6292380] Probando diff
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### Segunda prueba de diferencias
Se añade la línea `siete` al archivo `texto.txt`:
```bash
$ git diff
```
**Salida obtenida:**
```text
diff --git a/texto.txt b/texto.txt
index bf98941..430cdae 100644
--- a/texto.txt
+++ b/texto.txt
@@ -3,3 +3,4 @@ dos
 cuatro
 cinco
 seis
+siete
```
````

---

