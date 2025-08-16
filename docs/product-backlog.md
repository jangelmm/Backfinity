# **Product Backlog – BackFinity** 

-----

# Historias de Usuario:

## **HU1 – Respaldo desde terminal**

**Historia de Usuario:**
Como usuario, quiero ejecutar BackFinity desde la terminal con el comando de respaldo (`--backup`) para iniciar una copia de seguridad de una carpeta.

**Criterios de aceptación:**

  * El comando debe recibir la ruta de la carpeta a respaldar y un nombre único para el backup.
  * El sistema debe validar que la ruta de la carpeta existe y es accesible.
  * Si falta algún parámetro, debe mostrar un mensaje de error claro y la ayuda del comando.

**Tareas técnicas:**

  * Configurar un `parser` de argumentos para la CLI (`argparse` en Python).
  * Implementar la validación de la ruta de la carpeta.
  * Diseñar la estructura de los comandos `--backup` y `--restore`.

-----

## **HU2 – Encriptación de archivos**

**Historia de Usuario:**
Como usuario, quiero que mi carpeta de respaldo se encripte para proteger mi privacidad y seguridad.

**Criterios de aceptación:**

  * El sistema debe generar una clave de encriptación aleatoria y segura.
  * Debe usar un algoritmo de encriptación robusto (ej. **AES-256**).
  * El archivo de la carpeta comprimida debe encriptarse completamente antes de ser fragmentado.

**Tareas técnicas:**

  * Integrar la librería **`cryptography`** o **`PyCryptodome`**.
  * Implementar la función de generación de clave.
  * Crear la lógica de encriptación del archivo comprimido.

-----

## **HU3 – Fragmentación de archivos**

**Historia de Usuario:**
Como usuario, quiero que mi archivo encriptado se fragmente en partes de 2 GB para poder subirlas a Telegram sin problemas.

**Criterios de aceptación:**

  * El sistema debe dividir el archivo encriptado en fragmentos de tamaño máximo de 2 GB.
  * Cada fragmento debe tener un nombre único que incluya su posición (ej. `mi-backup-linux.part001.enc`).
  * El proceso de fragmentación debe ser eficiente para archivos muy grandes.

**Tareas técnicas:**

  * Implementar la lógica para leer el archivo en bloques y escribir nuevos archivos.
  * Implementar la convención de nombres para los fragmentos.
  * Agregar manejo de errores para problemas de espacio en disco.

-----

## **HU4 – Subida a Telegram**

**Historia de Usuario:**
Como usuario, quiero que los fragmentos de mi backup se suban automáticamente a un chat de Telegram.

**Criterios de aceptación:**

  * El sistema debe usar la API de Telegram para autenticarse y subir los archivos.
  * Cada fragmento debe subirse como un archivo independiente.
  * El sistema debe mostrar el progreso de subida de cada archivo.

**Tareas técnicas:**

  * Configurar y autenticar el bot de Telegram (`pyrogram` o `python-telegram-bot`).
  * Implementar la función de subida de archivos al chat o canal.
  * Agregar manejo de errores para casos de conexión o API.

-----

## **HU5 – Gestión del índice**

**Historia de Usuario:**
Como usuario, quiero que el sistema guarde la información de mi backup para poder restaurarlo más tarde.

**Criterios de aceptación:**

  * El sistema debe crear un archivo de índice (`.json`) con el nombre del backup, la clave de encriptación y la lista de fragmentos.
  * Este archivo debe guardarse localmente.
  * La clave de encriptación debe ser legible solo para el usuario.

**Tareas técnicas:**

  * Implementar las funciones de `guardar_indice()` y `cargar_indice()`.
  * Definir el esquema del archivo JSON para el índice.
  * Asegurar que la clave de encriptación se maneja de forma segura (por ahora, en texto plano si es de uso personal, pero con una advertencia).

-----

## **HU6 – Restauración de backup**

**Historia de Usuario:**
Como usuario, quiero que el sistema me permita restaurar una copia de seguridad completa desde Telegram.

**Criterios de aceptación:**

  * Al ejecutar el comando `--restore`, el sistema debe buscar los fragmentos por el nombre único del backup.
  * Debe descargar todos los fragmentos y unirlos en un solo archivo.
  * Debe desencriptar el archivo y restaurar la carpeta original.

**Tareas técnicas:**

  * Implementar la función de búsqueda de archivos en Telegram.
  * Desarrollar la lógica de descarga y unión de fragmentos.
  * Integrar la función de desencriptación.

-----

## **HU7 – Indicadores de progreso**

**Historia de Usuario:**
Como usuario, quiero ver un indicador de progreso para saber el estado de la encriptación, la subida y la restauración.

**Criterios de aceptación:**

  * Mostrar una barra de progreso para la encriptación y la fragmentación.
  * Mostrar el progreso de subida/descarga de cada archivo en la terminal.
  * Incluir mensajes de éxito al final de cada proceso.

**Tareas técnicas:**

  * Usar librerías de `tqdm` o similar.
  * Integrar la lógica de progreso en las funciones principales.

-----

## **HU8 – Verificación de integridad**

**Historia de Usuario:**
Como usuario, quiero que el sistema verifique la integridad de mi backup para asegurarme de que no se ha corrompido.

**Criterios de aceptación:**

  * El sistema debe calcular un **hash (ej. SHA-256)** del archivo original antes de encriptarlo y guardarlo en el índice.
  * Al restaurar el archivo, debe calcular el hash de la carpeta restaurada y compararlo con el original.
  * Si los hashes no coinciden, debe mostrar una advertencia al usuario.

**Tareas técnicas:**

  * Implementar la función para calcular el hash.
  * Agregar el campo de `hash` al archivo de índice.
  * Comparar los hashes al final del proceso de restauración.

-----

## **HU9 – Documentación inicial del proyecto**

**Historia de Usuario:**
Como usuario/desarrollador, quiero tener una documentación clara del proyecto para entender su funcionamiento y cómo usarlo.

**Criterios de aceptación:**

  * Un `README.md` que explique el propósito del proyecto.
  * Instrucciones de instalación y uso de la CLI.
  * Una breve guía de la arquitectura del proyecto.

**Tareas técnicas:**

  * Redactar los archivos de documentación (`README.md`, `docs/`).
  * Crear la tabla de contenido.
  * Agregar ejemplos de uso de los comandos.

-----

```csv
Título,Descripción,Etiqueta,Prioridad
HU1 – Respaldo desde terminal,"Como usuario, quiero ejecutar BackFinity desde la terminal con el comando de respaldo (--backup) para iniciar una copia de seguridad de una carpeta.",Sprint 1,Alta
HU2 – Encriptación de archivos,"Como usuario, quiero que mi carpeta de respaldo se encripte para proteger mi privacidad y seguridad.",Sprint 1,Alta
HU3 – Fragmentación de archivos,"Como usuario, quiero que mi archivo encriptado se fragmente en partes de 2 GB para poder subirlas a Telegram sin problemas.",Sprint 1,Alta
HU4 – Subida a Telegram,"Como usuario, quiero que los fragmentos de mi backup se suban automáticamente a un chat de Telegram.",Sprint 1,Alta
HU5 – Gestión del índice,"Como usuario, quiero que el sistema guarde la información de mi backup para poder restaurarlo más tarde.",Sprint 1,Alta
HU6 – Restauración de backup,"Como usuario, quiero que el sistema me permita restaurar una copia de seguridad completa desde Telegram.",Sprint 1,Alta
HU7 – Indicadores de progreso,"Como usuario, quiero ver un indicador de progreso para saber el estado de la encriptación, la subida y la restauración.",Sprint 1,Media
HU8 – Verificación de integridad,"Como usuario, quiero que el sistema verifique la integridad de mi backup para asegurarme de que no se ha corromido.",Sprint 2,Media
HU9 – Documentación inicial del proyecto,"Como usuario/desarrollador, quiero tener una documentación clara del proyecto para entender su funcionamiento y cómo usarlo.",Sprint 1,Media
```

-----

# Historias Épicas

## **E1 - Funcionalidad de respaldo y restauración**

Como usuario, quiero una solución completa y segura que me permita respaldar mis archivos grandes a Telegram y restaurarlos fácilmente en caso de que lo necesite.

HU1 - HU6

## **E2 - Robustez y usabilidad**

Como usuario, quiero que el sistema sea confiable, me dé un feedback claro del proceso y verifique la integridad de mis datos para asegurar que mi backup es 100% funcional.

HU7 - HU8