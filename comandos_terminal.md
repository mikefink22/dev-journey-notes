## **¿Dónde deberías estar posicionado para usar esos comandos?**

Para que los comandos de la terminal funcionen correctamente, siempre debes estar en el **directorio que contiene los archivos o carpetas** sobre los que quieres operar. La terminal siempre trabaja desde tu **directorio actual de trabajo**.

1.  **`cp *.js new_js_files/`**

      * **Propósito:** Copia todos los archivos con extensión `.js` al subdirectorio `new_js_files/`.
      * **Posición:** Debes estar en el directorio que **contiene los archivos `.js`** que quieres copiar. La carpeta `new_js_files/` debe existir y ser accesible desde donde te encuentras.
      * **Ejemplo:**
        ```
        MiProyecto/
        ├── scripts/         <-- Posiciónate aquí
        │   ├── app.js
        │   └── utils.js
        └── new_js_files/
        ```
        ```bash
        cd MiProyecto/scripts/
        cp *.js ../new_js_files/ # '..' sube un nivel para acceder a 'new_js_files'
        ```

2.  **`rm -rf old_module/`**

      * **Propósito:** Elimina una carpeta y todo su contenido de forma forzada y recursiva.
      * **Posición:** Debes estar en el directorio que **contiene la carpeta `old_module/`** que quieres eliminar.
      * **Ejemplo:**
        ```
        MiProyecto/          <-- Posiciónate aquí
        ├── src/
        └── old_module/      # Esta es la carpeta a eliminar
        ```
        ```bash
        cd MiProyecto/
        rm -rf old_module/
        ```

-----

## **Guía de Comandos Comunes en la Terminal (Git Bash)**

Aquí tienes los comandos más utilizados, con una breve descripción y ejemplos prácticos:

-----

### **1. Navegación (¿Dónde estoy y cómo me muevo?)**

  * **`pwd` (Print Working Directory)**

      * **Qué hace:** Muestra la **ruta absoluta** del directorio en el que te encuentras actualmente.
      * **Ejemplo:**
        ```bash
        pwd
        # Salida: /c/Users/TuUsuario/Documents/MiProyectoGit
        ```

  * **`ls` (List)**

      * **Qué hace:** Muestra el **contenido** (archivos y subdirectorios) del directorio actual.
      * **Opciones comunes:**
          * `-l`: Lista detallada (permisos, propietario, tamaño, fecha).
          * `-a`: Muestra todos los archivos, incluyendo los ocultos (como `.git`).
          * `-lh`: Lista detallada con tamaño legible para humanos (KB, MB, GB).
      * **Ejemplo:**
        ```bash
        ls
        # Salida: index.html css js README.md

        ls -la
        # Salida (ejemplo de contenido):
        # drwxr-xr-x  2 TuUsuario 4096 Jun 20 10:00 .
        # drwxr-xr-x 13 TuUsuario 4096 Jun 20 09:30 ..
        # drwxr-xr-x  2 TuUsuario 4096 Jun 19 15:20 .git
        # ... (otros archivos y directorios)
        ```
---

### **Desglosando la Salida de `ls -l`**

Cuando utilizas la opción `-l` con el comando `ls` (por ejemplo, `ls -l`), obtienes una lista detallada que incluye varias columnas de información para cada archivo o directorio. Vamos a desglosar cada una de estas columnas basándonos en una línea típica, como la de `index.html`:

`-rw-r--r-- 1 TuUsuario TuGrupo 1024 Jun 22 09:15 index.html`

#### **1. Permisos del Archivo/Directorio (`-rw-r--r--` o `drwxr-xr-x`)**

Esta es la primera y más compleja sección, que representa los **permisos de acceso** y el **tipo** del archivo o directorio.

* **Primer Carácter (`-` o `d`):** Indica el tipo de entrada.
    * `d`: Es un **directorio** (ej. `.git`, `css`, `js`).
    * `-`: Es un **archivo** regular (ej. `index.html`, `README.md`).
    * `l`: (Menos común aquí) Es un **enlace simbólico**.

* **Los 9 caracteres siguientes (`rwx r-x r-x`):** Se dividen en tres grupos de tres, que representan los permisos de **lectura (`r`)**, **escritura (`w`)** y **ejecución (`x`)**:
    * **Primer Grupo (`rwx`): Permisos para el Dueño/Propietario**
        * `r`: Permiso de **lectura** (read).
        * `w`: Permiso de **escritura** (write).
        * `x`: Permiso de **ejecución** (execute). Para directorios, significa que puedes *entrar* en ellos.
    * **Segundo Grupo (`r-x`): Permisos para el Grupo**
        * Los mismos permisos, pero para los usuarios que pertenecen al **grupo** propietario del archivo/directorio.
    * **Tercer Grupo (`r-x`): Permisos para Otros/Todos**
        * Los mismos permisos, pero para **cualquier otro usuario** en el sistema.

* **Ejemplo `index.html` (`-rw-r--r--`):**
    * Es un **archivo** (`-`).
    * El **dueño** puede leer y escribir (`rw-`).
    * Los miembros del **grupo** solo pueden leer (`r--`).
    * **Cualquier otra persona** solo puede leer (`r--`).

* **Ejemplo `css/` (`drwxr-xr-x`):**
    * Es un **directorio** (`d`).
    * El **dueño** puede leer, escribir y ejecutar/entrar (`rwx`).
    * Los miembros del **grupo** pueden leer y ejecutar/entrar (`r-x`).
    * **Cualquier otra persona** puede leer y ejecutar/entrar (`r-x`).

#### **2. Número de Enlaces Duros (`1`)**

* Para la mayoría de los archivos regulares, este número suele ser `1`.
* Para directorios, representa el número de subdirectorios que contiene, más dos enlaces implícitos (el enlace al propio directorio `.`, y al directorio padre `..`).

#### **3. Propietario/Dueño (`TuUsuario`)**

* El **nombre del usuario** que es el dueño del archivo o directorio.

#### **4. Grupo Propietario (`TuGrupo`)**

* El **nombre del grupo** al que pertenece el archivo o directorio.

#### **5. Tamaño en Bytes (`1024`)**

* El tamaño del archivo en **bytes**. Para directorios, a menudo muestra el tamaño del "bloque" en el disco, no el tamaño real acumulado de su contenido.

#### **6. Fecha y Hora de Última Modificación (`Jun 22 09:15`)**

* La fecha y hora en que el archivo o directorio fue **modificado por última vez**.

#### **7. Nombre del Archivo/Directorio (`index.html`)**

* El **nombre real** del archivo o directorio.

---

**En resumen:** Los caracteres como `drwxr-xr-x` y la serie de datos que les sigue en la salida de `ls -l` proporcionan una **vista detallada de los permisos, la propiedad, el tamaño y la fecha de modificación** de cada elemento. Esta información es fundamental en entornos Unix/Linux para entender cómo se gestiona el acceso y quién puede interactuar con los archivos y directorios.

---

  * **`cd` (Change Directory)**

      * **Qué hace:** Te permite **moverte** entre diferentes directorios.
      * **Ejemplos:**
          * **`cd NombreCarpeta`**: Entra en un subdirectorio.
            ```bash
            cd css/
            # Ahora estás en /c/Users/TuUsuario/Documents/MiProyectoGit/css
            ```
          * **`cd ..`**: Sube un nivel al directorio padre.
            ```bash
            cd ..
            # Ahora estás de nuevo en /c/Users/TuUsuario/Documents/MiProyectoGit
            ```
          * **`cd ~`**: Va a tu directorio personal (home).
          * **`cd /`**: Va a la raíz del sistema de archivos.
          * **`cd -`**: Vuelve al último directorio visitado.

-----

### **2. Creación y Eliminación**

  * **`mkdir` (Make Directory)**

      * **Qué hace:** Crea un nuevo **directorio** (carpeta).
      * **Ejemplo:**
        ```bash
        mkdir images                  # Crea una carpeta 'images'
        mkdir src/components          # Crea 'components' dentro de 'src' (si 'src' existe)
        mkdir -p src/utils/helpers    # Crea 'src', 'utils' y 'helpers' si no existen
        ```

  * **`touch`**

      * **Qué hace:** Crea un **archivo vacío** nuevo o actualiza la fecha de modificación de un archivo existente.
      * **Ejemplo:**
        ```bash
        touch nuevo_archivo.txt # Crea 'nuevo_archivo.txt'
        ```

  * **`rm` (Remove)**

      * **Qué hace:** Elimina **archivos**.
      * **Opciones comunes:**
          * `-r`: Elimina **directorios** y su contenido recursivamente.
          * `-f`: Fuerza la eliminación sin pedir confirmación (¡**usa con mucha precaución**\!).
      * **Ejemplo:**
        ```bash
        rm archivo_viejo.txt    # Elimina 'archivo_viejo.txt'
        rm -rf temp_folder/     # ¡Elimina la carpeta 'temp_folder' y todo su contenido sin preguntar!
        ```

-----

### **3. Copiar y Mover**

  * **`cp` (Copy)**

      * **Qué hace:** Copia **archivos** o **directorios**.
      * **Opción común:**
          * `-r`: Copia directorios recursivamente.
      * **Ejemplos:**
        ```bash
        cp archivo_original.txt archivo_copia.txt   # Copia un archivo
        cp styles.css css/style.css                 # Copia y renombra
        cp -r assets/ new_assets/                   # Copia una carpeta y su contenido
        ```

  * **`mv` (Move)**

      * **Qué hace:** **Mueve** archivos o directorios, o los **renombra** si el destino es un nuevo nombre en el mismo lugar.
      * **Ejemplos:**
        ```bash
        mv old_name.txt new_name.txt # Renombra un archivo
        mv config.ini settings/      # Mueve 'config.ini' a la carpeta 'settings'
        mv temp_files/ backup/       # Mueve la carpeta 'temp_files' a 'backup'
        ```

-----

### **4. Visualización de Contenido**

  * **`cat` (Concatenate and Print Files)**

      * **Qué hace:** Muestra el **contenido de uno o varios archivos** directamente en la terminal.
      * **Ejemplo:**
        ```bash
        cat README.md # Muestra el contenido del archivo README.md
        ```

  * **`less`**

      * **Qué hace:** Muestra el contenido de un archivo de forma **paginada** (ideal para archivos grandes). Presiona `q` para salir.
      * **Ejemplo:**
        ```bash
        less log_grande.txt # Abre el archivo para verlo página por página
        ```

-----

¡Espero que esta guía te sea muy útil\! Practicar estos comandos te dará una base sólida para trabajar de manera eficiente no solo con Git, sino con cualquier sistema de archivos desde la línea de comandos.

¿Hay algún otro comando o tarea que te genere dudas?
