
# **Design Thinking aplicado a BackFinity**

## **1. Descubrimiento / Empatía / Investigación (Divergencia)**

  * **Contexto detectado**: La mayoría de las soluciones de backup en la nube son:

      * Servicios de pago con suscripciones mensuales o anuales.
      * Tienen límites de almacenamiento que, si se exceden, requieren un costo adicional.
      * Pueden ser complejas para usuarios no técnicos que solo quieren una forma simple y segura de guardar sus archivos.
      * No siempre ofrecen un control total sobre dónde se guardan los datos o si estos están encriptados de forma segura.

  * **Necesidades de los usuarios**:

      * Un método gratuito y simple para hacer copias de seguridad de archivos grandes.
      * Una solución que utilice un servicio de almacenamiento en la nube ya familiar para el usuario, como Telegram.
      * La capacidad de encriptar los datos antes de subirlos para asegurar su privacidad.
      * Poder recuperar y restaurar los archivos de forma sencilla, sin importar si el equipo original falla.
      * Una herramienta de uso personal que no dependa de servidores externos y que sea fácilmente accesible desde distintas plataformas.

  * **Hallazgos clave**:

      * Telegram ofrece almacenamiento ilimitado y gratuito a través de canales y chats privados, con un límite de 2 GB por archivo, lo que lo convierte en un candidato ideal.
      * No existe una herramienta que automatice este proceso de forma sencilla: encriptar, fragmentar y subir a Telegram, y luego revertir el proceso.
      * La encriptación es una necesidad fundamental para que los usuarios confíen en el sistema, ya que los archivos se subirán a un servicio de terceros.

-----

## **2. Definición / Síntesis (Convergencia)**

  * **Problema a resolver**:
    *"Actualmente no existe una herramienta gratuita y de código abierto que permita a los usuarios hacer copias de seguridad de carpetas grandes, encriptando, fragmentando y subiendo los datos a su propio almacenamiento personal en la nube de Telegram para una posterior recuperación."*

  * **Oportunidad del proyecto**:

      * Crear una solución de respaldo personal, gratuita y con un control total de los datos por parte del usuario.
      * Aprovechar una infraestructura de almacenamiento ya existente y robusta como la de Telegram.
      * Ofrecer una experiencia de uso intuitiva tanto para la subida como para la recuperación de los archivos.
      * Desarrollar una aplicación de escritorio y una versión web para mayor accesibilidad.

-----

## **3. Ideación (Divergencia y Convergencia)**

  * **Lluvia de ideas de funciones iniciales**:

      * Recibir una carpeta como entrada.
      * Comprimir y encriptar la carpeta en un solo archivo.
      * Fragmentar el archivo en paquetes de 2 GB.
      * Subir cada fragmento a un canal o chat privado de Telegram usando un bot.
      * Guardar un índice local del backup con el nombre del proyecto, la clave y la lista de fragmentos.
      * Función de recuperación: buscar por el nombre, descargar los fragmentos, unirlos, desencriptarlos y restaurar la carpeta.
      * Una interfaz gráfica de usuario (GUI) para la versión de escritorio y una interfaz web para la versión de servidor.
      * Usar un **hash** del archivo original para verificar la integridad de la copia al restaurarla.

  * **Selección para la primera versión (MVP)**:

      * Desarrollar la funcionalidad básica en **Python** para la versión de escritorio, ya que cuenta con librerías robustas para la encriptación y la interacción con la API de Telegram.
      * Implementar las funciones de **subir y recuperar un solo backup**.
      * Añadir una interfaz de línea de comandos (CLI) simple para empezar, y luego construir la GUI.
      * El sistema de índice inicial se guardará en un archivo **`.json`** simple, localmente.

-----

## **4. Implementación / Construcción (Divergencia y Convergencia)**

  * **Primera iteración (v0.1)**:

      * Crear un script en Python que reciba una ruta de carpeta.
      * Integrar **`PyCryptodome`** para la encriptación AES y **`Pyrogram`** para la interacción con Telegram.
      * Implementar la fragmentación del archivo grande y la subida de cada fragmento.
      * Desarrollar la lógica de descarga y reensamblaje para la recuperación.
      * El índice del backup se guardará en un archivo `backfinity.json` en la misma carpeta de la herramienta.

  * **Pruebas y feedback**:

      * Probar la herramienta con carpetas de distintos tamaños, verificando que la restauración es exitosa y que el archivo original no se corrompe.
      * Validar que la encriptación funciona y que los archivos no pueden ser leídos sin la clave.

  * **Iteraciones siguientes**:

      * Desarrollar la interfaz gráfica de usuario (GUI) para el escritorio.
      * Crear la versión web con un framework como **Flask o Django**.
      * Agregar funcionalidades como la gestión de múltiples backups y un sistema de verificación de integridad más robusto.
      * Implementar un sistema para guardar el índice en Telegram junto a los fragmentos para mayor redundancia.