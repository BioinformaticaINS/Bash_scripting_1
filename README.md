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

### **2. Variables en Shell Scripting

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

- **Ejemplos comunes:**

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

---





























### **2. Creación de Scripts de Shell para Bioinformática**

#### **2.1. Estructura de un Script de Shell**
- **Shebang:** `#!/bin/bash`.
- **Comentarios:** `# Esto es un comentario`.
- **Variables:** `ruta="/ruta/al/directorio"`.
- **Ejecución de comandos:** `fastq-dump SRR123456`.

#### **2.2. Ejemplo de Script para Descargar Datos de SRA**
```bash
#!/bin/bash
# Descargar un archivo FASTQ desde SRA
ID="SRR123456"
fastq-dump $ID
echo "Descarga completada: $ID.fastq"
```

#### **2.3. Ejemplo de Script para Buscar y Descargar Datos de NCBI**
```bash
#!/bin/bash
# Buscar y descargar datos de NCBI
TERM="Homo sapiens[Organism] AND RNA-Seq[All Fields]"
esearch -db nucleotide -query "$TERM" | efetch -format fasta > datos.fasta
echo "Datos descargados: datos.fasta"
```

---

### **3. Automatización de Tareas con Variables y Bucles**

#### **3.1. Uso de Variables en Scripts**
- **Ejemplo:**
  ```bash
  #!/bin/bash
  ID="SRR123456"
  OUTPUT="resultados/$ID.fastq"
  fastq-dump $ID -O $OUTPUT
  echo "Archivo guardado en: $OUTPUT"
  ```

#### **3.2. Uso de Bucles para Procesar Múltiples Archivos**
- **Ejemplo:**
  ```bash
  #!/bin/bash
  # Descargar múltiples archivos FASTQ
  for ID in SRR123456 SRR654321 SRR987654
  do
    fastq-dump $ID
    echo "Descargado: $ID.fastq"
  done
  ```

---

### **4. Integración de Comandos Bioinformáticos en Scripts**

#### **4.1. Ejemplo de Script para Procesar Datos con `bio`**
```bash
#!/bin/bash
# Procesar datos con la herramienta bio
INPUT="datos.fasta"
OUTPUT="resultados/analisis.txt"
bio analyze $INPUT > $OUTPUT
echo "Análisis completado: $OUTPUT"
```

#### **4.2. Ejemplo de Script para Descargar y Procesar Datos**
```bash
#!/bin/bash
# Descargar y procesar datos
ID="SRR123456"
fastq-dump $ID
bio analyze $ID.fastq > analisis_$ID.txt
echo "Procesamiento completado: analisis_$ID.txt"
```

---

### **5. Práctica: Automatización de un Flujo de Trabajo Bioinformático**

#### **5.1. Descarga y Procesamiento de Datos de Secuenciación**
- **Paso 1:** Descargar archivos FASTQ desde SRA.
- **Paso 2:** Procesar los archivos FASTQ con herramientas bioinformáticas.
- **Paso 3:** Generar un informe de análisis.

#### **5.2. Ejemplo de Flujo de Trabajo Automatizado**
```bash
#!/bin/bash
# Flujo de trabajo automatizado
IDS=("SRR123456" "SRR654321" "SRR987654")
for ID in ${IDS[@]}
do
  # Descargar archivo FASTQ
  fastq-dump $ID
  
  # Procesar archivo FASTQ
  bio analyze $ID.fastq > analisis_$ID.txt
  
  # Generar informe
  echo "Análisis completado para $ID" >> informe.txt
done
echo "Flujo de trabajo completado."
```

---

### **6. Actividades Asincrónicas**

#### **6.1. Creación de un Script para Descargar Datos de NCBI**
- **Ejercicio:** Crear un script que busque y descargue secuencias de ADN de una especie específica utilizando `esearch` y `efetch`.

#### **6.2. Automatización de un Flujo de Trabajo**
- **Ejercicio:** Crear un script que descargue múltiples archivos FASTQ desde SRA, los procese con `bio`, y genere un informe de análisis.

---

### **7. Recursos Adicionales**
- **Bibliografía:**
  - Blum, R., & Bresnahan, C. (2021). *Linux Command Line and Shell Scripting Bible*. Wiley. Capítulo 11.
- **Documentación Oficial:**
  - `fastq-dump`: [SRA Toolkit Documentation](https://ncbi.github.io/sra-tools/).
  - `esearch` y `efetch`: [NCBI E-utilities Documentation](https://www.ncbi.nlm.nih.gov/books/NBK25499/).
  - `bio`: [Documentación de la herramienta bio](https://bio-tools.org/).

---

### **Conclusión**
- **Resumen:** Los estudiantes habrán aprendido a utilizar Shell scripting para automatizar tareas comunes en bioinformática, integrando comandos como `fastq-dump`, `esearch`, `efetch`, y `bio`.
- **Preguntas de Reflexión:**
  - ¿Cómo puede la automatización con Shell scripting mejorar la eficiencia en el análisis bioinformático?
  - ¿Qué otras tareas bioinformáticas podrían automatizarse utilizando scripts de Shell?

---

Esta clase combina los conceptos teóricos de Shell scripting con la aplicación práctica en bioinformática, permitiendo a los estudiantes trabajar con datos biológicos reales y automatizar flujos de trabajo complejos.
