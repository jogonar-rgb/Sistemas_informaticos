# Shell Scripts. Introducción.

1.  **Introducción a la programación shell**


La palabra shell en GNU/Linux hace referencia a diferentes cosas. En primer lugar, hace referencia al intérprete de órdenes que es la interfaz de usuario principal. Es el shell quien atiende a lo que se teclea y quien ejecuta las órdenes. Un segundo uso de la palabra tiene que ver con que el shell incluye un lenguaje de programación completo. Un programa escrito en shell se denomina **guión shell, programa shell** o simplemente un **shell**.

1.1.  **Ejecución de un guión.**

Después de crear el archivo (lo normal va a se mediante un editor de texto) hay que hacerlo ejecutable. Esto significa dar al archivo permisos de acceso para **lectura y ejecución**. Para hacer que el archivo sin.sh pueda ser leído y ejecutando, se usa la orden ***chmod +rx sin.sh***. Ahora puede **ejecutarse la orden tecleando el nombre del archivo ejecutable.**
Las diferencias más importantes entre las distintas formas de ejecutar guiones dependen de si el guión es ejecutado por el shell actual o por un subshell y de la forma en que las órdenes del guión se presentan al shell.
Cuando se ejecuta un guión escribiendo su nombre el shell crea un subshell que lee y ejecuta las órdenes del archivo.

!!! Note "Nota"
    Para hacer lo mismo explícitamente, ejecútese la orden sh dando el nombre del archivo como un argumento. Por ejemplo,
    !!! example "Ejemplo"
        ```shell
        sh sin.sh 
        ./sin.sh
        ```
    es una forma alternativa de ejecutar el guión sin.sh. La orden sh ejecuta un subshell, que realiza las órdenes del guión. El programa se ejecuta hasta que se terminan las órdenes del archivo, se recibe una señal de finalización, se encuentra un error sintáctico o se llega a una orden exit. Cuando el programa termina, el subshell muere y el shell original despierta y devuelve una petición de orden del sistema. De este modo, **cuando se ejecuta un guión de esta forma, el archivo debe tener permiso de acceso de lectura, pero no necesita ser ejecutable.**

!!! Note "Nota"
    A veces es conveniente ejecutar un guión pequeño sin colocar previamente las órdenes en un archivo. Puede teclearse una lista de órdenes y ejecutarlas en un subshell **colocando la lista entre paréntesis** ( ). Resulta útil cuando se quiere redirigir la salida del conjunto completo de órdenes a un archivo o a un fichero. Por ejemplo,
    !!! example "Ejemplo"
        ```shell
        (date; pwd; las) > contents 
        ```
    envía la fecha, el nombre del directorio actual y una lista de su contenido al archivo contents. Ejecutar órdenes dentro de un paréntesis (en un subshell independiente) puede usarse en los guiones shell, así como en la línea de órdenes. 

1.2.  **Comentarios en los guiones shell**
Se pueden insertar comentarios en los programas de shell utilizando **#**. Cuando el shell encuentra un palabra que comienza con #, ignora todo lo que existe desde ese carácter hasta el final de línea.
A esta regla se le añade una excepción:
   
??? example "Ejemplo"
    ```shell
    #!/bin/sh
    echo "Hola mundo"
    ```

    ??? note "Comentario"
        ```
        # Esto es un comentario
        ```


que indica el shell que será utilizado por el script, no un comentario. Esta línea debe ser la primera del fichero que contiene el script.

1.3.  **Argumentos en los programas shell**
Existe la posibilidad de enviar parámetros a los shell script. Cuando se ejecuta un programa shell, las variables shell se fijan automáticamente para que coincidan con los argumentos de la línea de órdenes dados al programa. Estas variables se conocen como **parámetros posicionales** y permiten al programa acceder y manipular información de la línea de órdenes.

* **$***: Muestra todos los parámetros
* **$#**: muestra el número de argumentos
* **$?**: contiene el valor de retorno del último mandato: cero si se ha ejecutado bien y se interpreta como verdadero. Distinto de cero si se ha ejecutado mal y se interpreta como falso (al contrario que el lenguaje C)
* **$!**: contiene el ID del proceso del último proceso subordinado. Resulta útil cuando un guión necesita eliminar un proceso subordinado que ha iniciado previamente.
* **$0**: es el nombre del programa shell.
* **$1,$2..$9**: parámetros pasados al script.
* La orden **SHIFT** desplaza a la izquierda los argumentos, perdiendo el de la izquierda y decrementando el número de los mismos.