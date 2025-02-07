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


## **1. ¿Qué es Shell Scripting?**
- **Definición:** Un script de Shell es un archivo que contiene una serie de comandos que se ejecutan en secuencia.
- **Aplicación en Bioinformática:** Automatización de tareas repetitivas, como la descarga de datos, procesamiento de secuencias, y análisis de datos.
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
