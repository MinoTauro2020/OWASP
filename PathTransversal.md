# Directory Traversal | Guía completa

 Directory Traversal, también conocido como Path Traversal, es una vulnerabilidad que permite a un atacante acceder a archivos y directorios fuera de la ubicación prevista. Esto ocurre cuando una aplicación no valida adecuadamente las entradas del usuario y permite caracteres especiales o secuencias de escape en las rutas de archivo. Los atacantes pueden aprovechar esto para navegar a través de directorios, leer archivos confidenciales e incluso ejecutar código malicioso.

## Lab #1: File path traversal, simple case
En este laboratorio, se presenta un caso simple de Directory Traversal. El objetivo es acceder a un archivo que se encuentra en una ubicación no deseada. Por ejemplo, si el archivo deseado está en /var/www/html/images/ y la aplicación no valida correctamente la entrada del usuario, un atacante podría proporcionar ../secrets/important.txt como entrada y obtener acceso al archivo.

Solución: Para mitigar este tipo de vulnerabilidad, la aplicación debe validar y sanitizar adecuadamente las rutas de archivo proporcionadas por el usuario. Se pueden utilizar funciones o bibliotecas específicas según el lenguaje de programación utilizado para evitar que los caracteres especiales o las secuencias de escape afecten la ruta de acceso real.

## Lab #2: File path traversal, traversal sequences blocked with absolute path bypass
En este laboratorio, se bloquean las secuencias de navegación como ../ para evitar el Directory Traversal básico. Sin embargo, aún es posible eludir estas restricciones utilizando rutas absolutas. Por ejemplo, si la aplicación bloquea ../ pero permite /var/www/html/, un atacante podría proporcionar /var/www/html/../secrets/important.txt como entrada para acceder al archivo deseado.

Solución: La solución es similar a la del Lab #1, pero en este caso, la aplicación también debe validar las rutas absolutas proporcionadas por el usuario y asegurarse de que no haya manipulación indebida de las rutas utilizando secuencias como ../.

## Lab #3: File path traversal, traversal sequences stripped non-recursively
En este laboratorio, la aplicación intenta eliminar las secuencias de navegación ../ de las rutas proporcionadas por el usuario, pero solo lo hace de forma no recursiva. Esto significa que las secuencias anidadas como ../../ aún pueden ser explotadas. Por ejemplo, si se proporciona ../../../secrets/important.txt como entrada, el atacante podría acceder al archivo.

Solución: La solución es similar a los laboratorios anteriores, pero en este caso, la aplicación debe realizar una eliminación recursiva de las secuencias de navegación ../ en la ruta proporcionada por el usuario antes de validarla o utilizarla para acceder a los archivos.

## Lab #4: File path traversal, traversal sequences stripped with superfluous URL-decode
En este laboratorio, la aplicación intenta eliminar las secuencias de navegación ../ del usuario. Sin embargo, se utiliza un decodificador URL que puede convertir %2e%2e%2f en ../. Esto permite a un atacante eludir la eliminación de las secuencias. Por ejemplo, si se proporciona %252e%252e%252e%252fsecrets%252fimportant.txt como entrada, el decodificador URL lo convierte en %2e%2e%2fsecrets%2fimportant.txt, que finalmente se interpreta como ../secrets/important.txt.

Solución: Para solucionar este problema, la aplicación debe realizar una eliminación adecuada de las secuencias de navegación ../ antes de aplicar cualquier decodificación URL. Además, se recomienda utilizar un enfoque de eliminación de caracteres especiales más amplio para evitar otras secuencias de escape que podrían utilizarse para eludir la seguridad.

## Lab #5: File path traversal, validation of start of path
En este laboratorio, la aplicación intenta validar el inicio de la ruta de acceso proporcionada por el usuario. Por ejemplo, podría requerir que la ruta de acceso comience con /var/www/html/ para ser considerada válida. Sin embargo, un atacante puede eludir esta restricción proporcionando una ruta de acceso que cumpla con los requisitos y luego use secuencias de navegación ../ para acceder a otros directorios.

Solución: Para mitigar este tipo de vulnerabilidad, la aplicación debe realizar una validación exhaustiva de toda la ruta de acceso proporcionada por el usuario, en lugar de solo verificar el inicio. Esto incluye la eliminación de secuencias de navegación ../ y la validación de cada componente de la ruta de acceso individualmente.

## Lab #6: File path traversal, validation of file extension with null byte bypass
En este laboratorio, la aplicación intenta validar la extensión de archivo proporcionada por el usuario. Sin embargo, si se permite la terminación de la extensión de archivo con un byte nulo (%00), un atacante puede eludir la validación y acceder a archivos no deseados. Por ejemplo, si se bloquea la extensión .txt pero se permite .txt%00, el atacante podría proporcionar important.txt%00 como entrada y acceder al archivo.

Solución: Para resolver este problema, la aplicación debe asegurarse de que las extensiones de archivo proporcionadas por el usuario se validen adecuadamente y se eliminen los caracteres no deseados, como el byte nulo (%00). Además, se recomienda utilizar una lista blanca de extensiones permitidas en lugar de una lista negra de extensiones bloqueadas.
