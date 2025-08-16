# **Lean Startup aplicado a BackFinity** 

## **1. Hipótesis**

  * **Hipótesis de problema**: Los usuarios necesitan una solución simple y gratuita para hacer copias de seguridad de sus archivos grandes, pero las herramientas existentes son costosas, complicadas o no ofrecen un control total sobre la privacidad y el almacenamiento.

  * **Hipótesis de solución**: Un sistema que empaquete, encripte, fragmente y suba archivos a Telegram, aprovechando su almacenamiento ilimitado y gratuito, será una solución atractiva para los usuarios, siempre y cuando el proceso sea automatizado y la recuperación sea sencilla.

-----

## **2. Producto Mínimo Viable (MVP)**

  * **Funcionalidad mínima**:

    1.  Un script de **línea de comandos (CLI)** en Python que reciba una ruta de carpeta como entrada.
    2.  Encriptar y fragmentar la carpeta en archivos de **2 GB**.
    3.  Subir los fragmentos a un canal de Telegram usando un **bot**.
    4.  Guardar un archivo de índice **local** con la información para la recuperación.
    5.  Un comando para **recuperar** los archivos, que los descargue, una, desencripte y restaure la carpeta original.

  * **Experiencia mínima**:

      * Un par de comandos básicos:
        ```bash
        python backfinity.py --backup "/ruta/a/mi/carpeta" --nombre "mi-backup-linux"
        python backfinity.py --restore "mi-backup-linux"
        ```
      * Feedback en la terminal sobre el progreso de la encriptación, fragmentación y subida de archivos (ej. "Subiendo fragmento 1 de 5...").

-----

## **3. Métricas de Éxito (MVP)**

  * **Cuantitativas**:

      * **Número de usuarios beta**: ¿Cuántas personas están dispuestas a probar la herramienta?
      * **Cantidad de repositorios clonados o descargas directas**.
      * **Número de *issues***: ¿Cuántos errores se reportan y con qué frecuencia?
      * **Uso de la herramienta**: ¿Los usuarios la usan para subir y para restaurar archivos?

  * **Cualitativas**:

      * **Comentarios y sugerencias**: ¿Qué tan fácil de usar es la herramienta? ¿Qué nuevas funcionalidades se piden?
      * **Satisfacción del usuario**: ¿Los usuarios que restauran sus archivos logran hacerlo exitosamente y sin problemas?

-----

## **4. Ciclo de Validación**

1.  **Construir** → Crear el MVP con la funcionalidad de respaldo y restauración mediante la CLI.
2.  **Medir** → Compartir el proyecto en **GitHub**, foros de programación y comunidades de Telegram.
3.  **Aprender** → Recopilar el feedback de los primeros usuarios. Decidir si el foco debe ser en mejorar la CLI, crear una **GUI de escritorio** o empezar a trabajar en la versión web. Si la respuesta es positiva, la próxima fase sería construir la interfaz gráfica.