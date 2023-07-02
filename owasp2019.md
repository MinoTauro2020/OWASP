# OWASP Top 10 API Security Risks - 2019

## API1:2019 - Broken Object Level Authorization

Las APIs tienden a exponer puntos finales que manejan identificadores de objetos, creando una amplia superficie de ataque de problemas de Control de Acceso a Nivel de Objeto. Se deben considerar verificaciones de autorización a nivel de objeto en cada función que acceda a una fuente de datos utilizando una ID del usuario.

**Ejemplo Práctico:**

Un atacante modifica el identificador de objeto en una solicitud de API para acceder a recursos a los que no tiene autorización.

**Medidas de Mitigación:**

- Implementar validación y filtrado de identificadores de objetos proporcionados por los usuarios.
- Realizar comprobaciones de autorización en cada función que acceda a datos utilizando identificadores de objetos.

## API2:2019 - Broken User Authentication

Los mecanismos de autenticación a menudo se implementan de manera incorrecta, lo que permite a los atacantes comprometer tokens de autenticación o explotar fallas de implementación para asumir temporal o permanentemente la identidad de otros usuarios. Comprometer la capacidad del sistema para identificar al cliente/usuario compromete la seguridad de la API en general.

**Ejemplo Práctico:**

Un atacante aprovecha una falla en el mecanismo de autenticación para suplantar la identidad de otro usuario.

**Medidas de Mitigación:**

- Implementar prácticas seguras de autenticación, como el uso de algoritmos de hash fuertes y la protección adecuada de los tokens de autenticación.
- Realizar pruebas de seguridad y revisiones de código para identificar y corregir vulnerabilidades en el proceso de autenticación.

## API3:2019 - Excessive Data Exposure

Al buscar implementaciones genéricas, los desarrolladores tienden a exponer todas las propiedades del objeto sin considerar su sensibilidad individual, confiando en que los clientes realicen la filtración de datos antes de mostrarlos al usuario.

**Ejemplo Práctico:**

Una API devuelve información sensible que no ha sido adecuadamente filtrada o protegida.

**Medidas de Mitigación:**

- Implementar mecanismos de filtrado y enmascaramiento de datos para exponer solo la información necesaria para cada usuario o solicitud.
- Realizar una revisión exhaustiva de los objetos y las propiedades expuestas por la API para asegurarse de que no se revele información confidencial.

## API4:2019 - Lack of Resources & Rate Limiting

Con frecuencia, las APIs no imponen restricciones en el tamaño o número de recursos que pueden ser solicitados por el cliente/usuario. Esto no solo puede afectar el rendimiento del servidor de la API, lo que lleva a una Denegación de Servicio (DoS), sino que también deja la puerta abierta a fallas de autenticación, como el ataque de fuerza bruta.

**Ejemplo Práctico:**

Un atacante realiza numerosas solicitudes a la API sin restricciones, agotando los recursos y afectando la disponibilidad de la API.

**Medidas de Mitigación:**

- Implementar límites de velocidad y restricciones en el número de solicitudes que un cliente/usuario puede realizar en un período de tiempo determinado.
- Realizar un monitoreo constante del rendimiento de la API para detectar y mitigar posibles ataques de denegación de servicio.

## API5:2019 - Broken Function Level Authorization

Las políticas de control de acceso complejas con diferentes jerarquías, grupos y roles, y una separación poco clara entre funciones administrativas y regulares, suelen llevar a fallas de autorización. Al explotar estos problemas, los atacantes obtienen acceso a los recursos de otros usuarios y/o funciones administrativas.

**Ejemplo Práctico:**

Un atacante accede a funciones o recursos a los que no tiene autorización legítima debido a fallas en el control de acceso.

**Medidas de Mitigación:**

- Implementar políticas de control de acceso granulares y revisar regularmente los permisos y roles asignados a los usuarios.
- Realizar pruebas exhaustivas de autorización para identificar y corregir fallas en el control de acceso.

## API6:2019 - Mass Assignment

La asignación de datos proporcionados por el cliente (por ejemplo, JSON) a modelos de datos, sin una filtración adecuada de propiedades basada en una lista blanca, suele llevar a la asignación masiva. Adivinar las propiedades de los objetos, explorar otros puntos finales de la API, leer la documentación o proporcionar propiedades de objeto adicionales en las cargas útiles de las solicitudes permite a los atacantes modificar propiedades de objetos a las que no deberían tener acceso.

**Ejemplo Práctico:**

Un atacante manipula los datos de entrada para asignar propiedades a objetos que normalmente no debería poder modificar.

**Medidas de Mitigación:**

- Implementar una lista blanca de propiedades permitidas en las solicitudes de asignación para evitar la manipulación de propiedades no deseadas.
- Validar y filtrar adecuadamente los datos de entrada antes de asignarlos a objetos o modelos de datos.

## API7:2019 - Security Misconfiguration

La configuración incorrecta de la seguridad es comúnmente el resultado de configuraciones predeterminadas no seguras, configuraciones incompletas o ad hoc, almacenamiento en la nube abierto, encabezados HTTP mal configurados, métodos HTTP innecesarios, uso permisivo de recursos compartidos de origen cruzado (CORS) y mensajes de error detallados que contienen información sensible.

**Ejemplo Práctico:**

Una API tiene configuraciones de seguridad incorrectas, como encabezados HTTP mal configurados o almacenamiento en la nube abierto.

**Medidas de Mitigación:**

- Revisar y asegurar la configuración predeterminada de la API y los servicios subyacentes.
- Aplicar las mejores prácticas de configuración de seguridad, como configurar adecuadamente los encabezados HTTP, restringir los métodos y recursos innecesarios, y minimizar la exposición de información confidencial en los mensajes de error.

## API8:2019 - Injection

Las vulnerabilidades de inyección, como SQL, NoSQL, inyección de comandos, etc., ocurren cuando datos no confiables se envían a un intérprete como parte de un comando o consulta. Los datos maliciosos del atacante pueden engañar al intérprete para que ejecute comandos no deseados o acceda a datos sin la autorización adecuada.

**Ejemplo Práctico:**

Un atacante inyecta código malicioso en una solicitud de API que es interpretado y ejecutado por la aplicación.

**Medidas de Mitigación:**

- Utilizar consultas parametrizadas o declarativas en lugar de construir consultas dinámicamente con datos no confiables.
- Validar y filtrar adecuadamente los datos de entrada para evitar la ejecución de comandos no deseados.

## API9:2019 - Improper Assets Management

Las APIs tienden a exponer más puntos finales que las aplicaciones web tradicionales, lo que hace que la documentación adecuada y actualizada sea de vital importancia. También es importante mantener un inventario de los hosts y versiones de API implementadas para mitigar problemas como versiones obsoletas de la API o puntos finales de depuración expuestos.

**Ejemplo Práctico:**

Una API tiene puntos finales obsoletos o expuestos innecesariamente que pueden ser aprovechados por un atacante.

**Medidas de Mitigación:**

- Mantener una documentación detallada y actualizada de la API, incluyendo información sobre los puntos finales, sus funciones y restricciones de acceso.
- Realizar auditorías regulares de la API para identificar y eliminar puntos finales obsoletos o expuestos innecesariamente.

## API10:2019 - Insufficient Logging & Monitoring

La falta de registros y monitoreo, junto con la falta de integración efectiva con la respuesta a incidentes, permite a los atacantes continuar atacando sistemas, mantener la persistencia, pivotar hacia otros sistemas para manipular, extraer o destruir datos. La mayoría de los estudios de violaciones demuestran que el tiempo necesario para detectar una violación supera los 200 días, y generalmente es detectado por partes externas en lugar de los procesos o monitoreo internos.

**Ejemplo Práctico:**

Una API carece de registros adecuados y monitoreo, lo que dificulta la detección oportuna de actividades maliciosas.

**Medidas de Mitigación:**

- Implementar un sistema de registro robusto que registre eventos de seguridad relevantes y actividades sospechosas.
- Establecer mecanismos de monitoreo proactivo que alerten sobre posibles violaciones o anomalías en el comportamiento de la API.

Estas son las medidas de mitigación recomendadas para abordar los riesgos de seguridad de API del OWASP Top 10 2019. Recuerda adaptar estas medidas a tu contexto específico y realizar pruebas de seguridad periódicas para identificar y corregir posibles vulnerabilidades.
