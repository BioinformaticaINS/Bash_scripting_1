# Bash scripting 1

## **Objetivo de la Clase:**

Al finalizar la clase, los estudiantes serán capaces de:
1. Comprender los conceptos básicos de Shell scripting.
2. Automatizar tareas comunes en bioinformática, como la descarga y procesamiento de datos.

---

### **1. Introducción a la Programación en Shell**

#### **1.1. ¿Qué es Shell?**

- **Definición:** El Shell es un intérprete de comandos que actúa como interfaz entre el usuario y el kernel del sistema operativo.
- **Funcionalidad:** Permite ejecutar comandos, automatizar tareas y gestionar procesos.

![](https://i.sstatic.net/LBRdx.png)

#### **1.2. Tipos de Shell**

- **Bourne Shell (sh):** La primera Shell tradicional de UNIX.
- **Korn Shell (ksh):** Amplía el Shell del sistema con características como historial de comandos y edición en línea.
- **Bourne Again Shell (bash):** El Shell más moderno y utilizado, desarrollado para el Proyecto GNU.
- **C Shell (csh):** Popular en sistemas BSD, diseñado para programadores en C.
- **Tenex C Shell (tcsh):** Mejora de csh con mayor velocidad y funcionalidades.

```bash
more /etc/shells

# Si deseamos instalar un Shell usamos la línea de comandos: sudo apt install <shell>.
```

¿Cuál es mi Shell?

```bash
echo $SHELL
```

¿Cuál es la versión de la shell ?

```bash
echo $BASH_VERSION
```

¿Puedo cambiar de Shell?

Sí. ¿Cómo?

```bash
# Sintaxis: $chsh <opciones> <usuario>
sudo chsh -s /bin/  # tabuleamos
```

#### **1.3. ¿Por qué usar Shell Scripting?**

- Permite automatizar tareas repetitivas y así ahorrar tiempo.
- Proporcionan una secuencia de actividades bien estructurada,modular y formateada.Un script es como una receta. 
- Permite introducir **valores dinámicos** a los diferentes comandos mediante el uso de argumentos por la línea de comandos.

```bash
$ rev
hola
aloh
user
resu
...
```

- Puede simplificar comandos complejos en una sola unidad en ejecución.
- Una vez creado, se puede ejecutar cualquier cantidad de veces por cualquier persona.*“Construye una vez y ejecuta muchas veces”.*

#### **1.4. Herramientas para Escribir Scripts**

- **Editores de texto:** Visual Studio Code, Sublime Text, VIM, Pluma.
- **Ejemplos de comandos básicos:** `rev`, `echo`, `pwd`.

#### **1.5. Shebang**

```
#!/bin/bash --> La primera línea del script le indica al sistema que tiene que usar shell BASH

#Fecha de escritura: 13/10/2022 --> Comentario  

#Este programa te informa en que directorio se encuentra trabajando la terminal. --> Comentario

lugar=$(pwd) # Variable

echo "en este momento te encuentras trabajando en este $lugar, no vayas a perderte"
```

### **2. Variables en Shell Scripting**

#### **2.1. ¿Qué es una Variable?**

- **Definición:** Una variable es una ubicación en memoria que almacena un valor.
- **Sintaxis básica:** `variable=valor`.
- **Características:** Dinámicas, modificables, y pueden almacenar múltiples tipos de datos.
  
```
# Variable: Crear, Modificar, Guardar y Eliminar
# Valor: Naturaleza múltiple, Dinámicos

nomre = "usuario"
edad = 44
ruta_archivos = "home/insuser/Proyecto_NGS"
```

#### **2.2. Tipos de Variables**

- **Variables Locales:** Accesibles solo en el Shell o sub-Shell donde se definieron.
- **Variables Globales:** Accesibles desde cualquier Shell o sub-Shell.

#### **2.3. Creación y Manipulación de Variables**

- **Variables Locales:** Accesibles solo en el shell o sub-shell donde se definió.
  
  - Ejemplo: `mi_nombre="ins"`.
  - Acceso: `echo $mi_nombre`.
    
- **Variables Globales:** Accesibles para cualquier en ejecución desde el shell o desde cualquier sub-shell generada a partir de ella.
  
  - Uso del comando `export`: `export saludo="Hola a todos"`.
  - Eliminación: `unset saludo`.

#### **2.4. Variables de Entorno Globales**

  - Las variables de entorno globales se establecen cuando se inicia una sesión.
  - Por convención, se suelen definir en letras mayúsculas para diferenciarlas de las variables que define el usuario.
  
| Variable | Descripción                                                      |
|----------|------------------------------------------------------------------|
| DISPLAY  | Donde aparecen las salidas de X-Windows                          |
| HOME     | Directorio personal                                              |
| HOSTNAME | Nombre de la máquina                                             |
| MAIL     | Archivo de correo                                                |
| PATH     | Lista de directorio en donde buscará programas y comandos        |
| PS1      | Prompt o indicador del shell que aparece en la línea de comandos |
| SHELL    | Interprete de comandos por defecto                               |
| TERM     | Tipo de terminal                                                 |
| USER     | Nombre de usuario                                                |

- **Cómo ver el contenido de una variable de entorno:** `echo $HOME` o `printenv HOME`

- Comando `printenv`

  ```
  printenv | head
  ```

#### **2.5. Nomenclatura de Variables**

- **Reglas:**
  
  - Solo caracteres alfanuméricos y guiones bajos (`_`).
  - No pueden contener espacios.
  - Sensibilidad a mayúsculas y minúsculas.
    
- **Convenciones:**
  
  - Variables de entorno en mayúsculas.
  - Otras variables en minúsculas.

#### **2.6. Expansión de Variables y Comandos**

- **Expansión de comandos:**
  
  - Sintaxis: `$(comando)` o `` `comando` ``.
  - Ejemplo: `user=$(whoami)`.
    
- **Operaciones aritméticas:**
  
  - Sintaxis: `$((expresión))`.
  - Ejemplo: `suma=$((1+1))`.

#### **2.7. Comillas Simples y Dobles**
- **Comillas Dobles (`" "`):** Permiten la expansión de variables.
- **Comillas Simples (`' '`):** Mantienen el valor literal, sin expansión.

```bash
(base) ins_user@VirtualBox:~$var=10
(base) ins_user@VirtualBox:~$echo "El valor de la variable $var"
El valor de la variable 10
(base) ins_user@VirtualBox:~$echo 'El valor de la variable $var'
El valor de la variable $var
```

Ejericio:

```
(base) ins_user@VirtualBox:~$var=10

El nombre de la varible es 10_1 
```

### **2.8. Variable de entorno PATH** 

Los directorios en el PATH se encuentran separados por dos puntos (:)

```bash
(base) ins_user@VirtualBox:~$ printenv PATH
/home/ins_user/miniconda3/bin:/home/ins_user/miniconda3/condabin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin:/usr/local/go/bin:/home/ins_user/go/bin
```


```bash
(base) ins_user@VirtualBox:~$ which pwd
/usr/bin/pwd
```

 - Búsqueda secuencial.
 - De no estar en ninguno de los directorios listados entonces se producirá un mensaje de error


### **2.9. ¿Cómo agregamos un directorio al PATH?**

```bash
export PATH=$PATH:/ruta
```

Ejemplo:

```bash
export PATH=$PATH:/home/ins_user/sra_tools/bin
```

- `export`: Comando que nos permite crear o modificar una variable de entorno global.
- `PATH`: Variable de entorno a crear o modificar.
- `=`: Operador de asignación.
- `$PATH`: Valor actual de la variable de entorno (antes de su modificación)
- `:/home/ins_user/sra_tools/bin`: Ruta absoluta que agregamos a la variable de entorno PATH

Para tener el directorio al final del PATH:

`export PATH=$PATH:/home/paula.soler/sra_tools/bin`

Para tener el directorio al inicio del PATH:

`export PATH=/home/paula.soler/sra_tools/bin:$PATH`

## 3. Interaccionando con SHELL y SUBSHELLs

### 3.1. Uso del comando `bash`

```bash
(base) ins_user@VirtualBox:~$                # Shell principal
(base) ins_user@VirtualBox:~$ bioinfo=9.25
(base) ins_user@VirtualBox:~$ bash           # Shell secuendatio
(base) ins_user@VirtualBox:~$ echo $bioinfo
(base) ins_user@VirtualBox:~$ exit
Exit
(base) ins_user@VirtualBox:~$ echo $bioinfo
9.25
```

Dato: *No pensemos que una sub-shell como una nueva ventana de terminal*

### 3.2. Creando subshells anidadas

```bash
(base) ins_user@VirtualBox:~$ export VAR=10
(base) ins_user@VirtualBox:~$ bash
(base) ins_user@VirtualBox:~$ echo $VAR
10
(base) ins_user@VirtualBox:~$ export VAR=20
(base) ins_user@VirtualBox:~$ echo $VAR
20
(base) ins_user@VirtualBox:~$ bash
(base) ins_user@VirtualBox:~$ echo $VAR
20
(base) ins_user@VirtualBox:~$ exit
exit
(base) ins_user@VirtualBox:~$ echo $VAR
20
(base) ins_user@VirtualBox:~$ exit
exit
(base) ins_user@VirtualBox:~$ echo $VAR
10
```

1. Creación de subshells anidadas.
2. Después de exportar una variable global, permanece exportada a todas las subcapas creadas posteriormente.
3. Puede cambiar el valor de la variable exportada en una subcapa. El valor modificado se pasará a las subcapas posteriores, pero si sale y vuelve a la capa original, se conserva el valor original.


### 3.3. Comparando variables locales Vs. globales 

```bash
(base) ins_user@VirtualBox:~$ drink="tea"
(base) ins_user@VirtualBox:~$ echo $drink
tea
(base) ins_user@VirtualBox:~$ bash # Abriendo una sub-shell
(base) ins_user@VirtualBox:~$ echo $drink
(base) ins_user@VirtualBox:~$ exit # ctrl + D
(base) ins_user@VirtualBox:~$ echo $drink
tea
(base) ins_user@VirtualBox:~$ export drink
$ bash
$ printenv drink
tea
(base) ins_user@VirtualBox:~$ exit
```

### 3.4. Scripts en la subshell

```bash
(base) ins_user@VirtualBox:~$ cat impresion.sh
var=LHB
echo $var
(base) ins_user@VirtualBox:~$ bash impresion.sh
LHB
(base) ins_user@VirtualBox:~$ sh impresion.sh
LHB
```

```bash
(base) ins_user@VirtualBox:~$ cat impresion.sh
echo $var
(base) ins_user@VirtualBox:~$ var=LHB
(base) ins_user@VirtualBox:~$ bash impresion.sh
```

** *Los scripts se ejecutan por defecto en una sub-shell* **

```bash
(base) ins_user@VirtualBox:~$ cat impresion.sh
echo $var
(base) ins_user@VirtualBox:~$ var=LHB
(base) ins_user@VirtualBox:~$ bash impresion.sh

(base) ins_user@VirtualBox:~$ .impresion.sh   # .script
```
---

## **4. Creación de Scripts de Shell para Bioinformática**

### **4.1. Estructura de un Script de Shell**

- **Shebang:** `#!/bin/bash`.
- **Comentarios:** `# Esto es un comentario`.
- **Variables:** `ruta="/ruta/al/directorio"`.
- **Ejecución de comandos:** `fastq-dump SRR123456`.

### **4.2. Ejemplo de Script para Descargar Datos de SRA**

```bash
#!/bin/bash
# Descargar un archivo FASTQ desde SRA
ID="SRR1553607"
fastq-dump --split-files -X 10000 $ID
echo "Descarga completada: $ID.fastq"
```

### **4.3. Ejemplo de Script para Buscar y Descargar Datos de NCBI**

```bash
#!/bin/bash
# Buscar y descargar datos de NCBI
TERM="Homo sapiens[Organism] AND RNA-Seq[All Fields]"
esearch -db nucleotide -query "$TERM" | efetch -format fasta > datos.fasta
echo "Datos descargados: datos.fasta"
```

### **4.4. Automatización de Tareas con Variables y Bucles**

  ```bash
  #!/bin/bash
  ID="SRR1553607"
  OUTPUT="raw_data/$ID.fastq"
  fastq-dump --split-files -X 10000 $ID -O $OUTPUT
  echo "Archivo guardado en: $OUTPUT"
  ```

#### **4.5. Uso de Bucles para Procesar Múltiples Archivos**

  ```bash
  #!/bin/bash
  # Descargar múltiples archivos FASTQ
  for ID in SRR1972948 SRR1972956 SRR1972955
  do
    fastq-dump --split-files -X 10000 $ID
    echo "Descargado: $ID.fastq"
  done
  ```

#### **4.3. Flujo de Trabajo Automatizado**
```bash
#!/bin/bash
# Flujo de trabajo automatizado
IDS=("SRR1972948" "SRR1972956" "SRR1972955")
for ID in ${IDS[@]}
do
  # Descargar archivo FASTQ
  fastq-dump --split-files -X 10000 $ID
  
  # Procesar archivo FASTQ
  bio analyze $ID.fastq > analisis_$ID.txt
  
  # Generar informe
  echo "Análisis completado para $ID" >> informe.txt
done
echo "Flujo de trabajo completado."
```
