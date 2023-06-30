# OWASP Top 10 API Security Risks - 2023

## API1:2023 - Autorización de Nivel de Objeto Rota (Broken Object Level Authorization)
Las APIs tienden a exponer puntos finales que manejan identificadores de objetos, creando una amplia superficie de ataque de problemas de Control de Acceso a Nivel de Objeto. Se deben considerar verificaciones de autorización a nivel de objeto en cada función que acceda a una fuente de datos utilizando una ID del usuario.

Ejemplo Práctico:
Un atacante modifica el identificador de un objeto en una solicitud API para acceder a datos de otro usuario. Por ejemplo, un atacante cambia el ID del objeto en una solicitud GET para obtener información confidencial de otro usuario.

Cómo Asegurarlo:
- Implementar controles de autorización sólidos a nivel de objeto.
- Validar que el usuario tiene acceso a los objetos solicitados antes de procesar la solicitud.

## API2:2023 - Autenticación Rota (Broken Authentication)
Con frecuencia, los mecanismos de autenticación se implementan incorrectamente, lo que permite a los atacantes comprometer tokens de autenticación o explotar fallas de implementación para asumir temporal o permanentemente la identidad de otros usuarios. Comprometer la capacidad del sistema para identificar al cliente/usuario compromete la seguridad de la API en general.

Ejemplo Práctico:
Un atacante intercepta un token de sesión no cifrado enviado en una solicitud API y lo utiliza para realizar acciones en nombre del usuario autenticado, como acceder a información confidencial o realizar cambios no autorizados.

Cómo Asegurarlo:
- Utilizar métodos de autenticación sólidos, como tokens de autenticación basados en estándares modernos.
- Implementar medidas de protección, como cifrado y firmado de tokens de autenticación.

## API3:2023 - Autorización de Nivel de Propiedad de Objeto Rota (Broken Object Property Level Authorization)
Esta categoría combina la exposición excesiva de datos (API3:2019 Excessive Data Exposure) y la asignación masiva (API6:2019 Mass Assignment), centrándose en la causa principal: la falta de validación de autorización o una validación inadecuada a nivel de propiedad de objeto. Esto conduce a la exposición o manipulación de información por parte de terceros no autorizados.

Ejemplo Práctico:
Una API permite a los usuarios enviar solicitudes POST para actualizar sus perfiles, pero no valida adecuadamente qué propiedades se pueden actualizar. Un atacante puede aprovechar esto y enviar una solicitud POST para actualizar propiedades adicionales, como roles de usuario, ganando así privilegios no autorizados.

Cómo Asegurarlo:
- Implementar validación y control de autorización en función de los permisos y propiedades permitidas para actualizaciones de objetos.
- Evitar la asignación masiva permitiendo solo la actualización de propiedades específicas y autorizadas.

## API4:2023 - Consumo No Restringido de Recursos (Unrestricted Resource Consumption)
Satisfacer las solicitudes de la API requiere recursos como ancho de banda de red, CPU, memoria y almacenamiento. Otros recursos, como correos electrónicos/SMS/llamadas telefónicas o validación biométrica, están disponibles a través de proveedores de servicios mediante integraciones de API y se pagan por solicitud. Los ataques exitosos pueden provocar una denegación de servicio o un aumento de los costos operativos.

Ejemplo Práctico:
Un atacante envía repetidamente solicitudes de API que requieren una gran cantidad de recursos, como la generación de informes complejos o el envío de numerosos correos electrónicos. Esto agota los recursos disponibles y afecta negativamente la disponibilidad y el rendimiento de la API.

Cómo Asegurarlo:
- Establecer límites y controles de uso para recursos específicos de la API.
- Implementar mecanismos de monitoreo y detección para identificar actividades anómalas y abusivas.

## API5:2023 - Autorización de Nivel de Función Rota (Broken Function Level Authorization)
Las políticas de control de acceso complejas con diferentes jerarquías, grupos y roles, y una separación poco clara entre funciones administrativas y regulares, tienden a generar fallas de autorización. Al explotar estas fallas, los atacantes pueden acceder a los recursos de otros usuarios y/o funciones administrativas.

Ejemplo Práctico:
Un atacante encuentra una API que maneja solicitudes de administración y descubre que no hay una validación adecuada de autorización para asegurarse de que solo los administradores puedan acceder a esas funciones. El atacante utiliza esta falla para ejecutar acciones de administración sin privilegios.

Cómo Asegurarlo:
- Establecer controles de autorización claros y coherentes en función de las funciones y privilegios requeridos.
- Realizar una separación adecuada entre funciones administrativas y regulares, evitando mezclar funcionalidades en una misma API.

## API6:2023 - Acceso No Restringido a Flujos de Negocio Sensibles (Unrestricted Access to Sensitive Business Flows)
Las APIs vulnerables a este riesgo exponen un flujo de negocio, como comprar un boleto o publicar un comentario, sin considerar cómo la funcionalidad podría perjudicar al negocio si se utiliza de manera excesiva de forma automatizada. Esto no necesariamente se debe a errores de implementación.

Ejemplo Práctico:
Una API permite la compra de boletos sin restricciones y no tiene medidas para limitar la cantidad de solicitudes que un único usuario puede enviar. Un atacante automatiza solicitudes de compra de boletos, agotando el inventario y afectando la disponibilidad para otros usuarios legítimos.

Cómo Asegurarlo:
- Implementar mecanismos de protección, como límites de frecuencia y límites de uso, para evitar el abuso automatizado de los flujos de negocio sensibles.
- Monitorear y analizar los patrones de uso para detectar actividades sospechosas y abusivas.

## API7:2023 - Falsificación de Petición del Lado del Servidor (Server Side Request Forgery)
Las fallas de Falsificación de Petición del Lado del Servidor (SSRF) pueden ocurrir cuando una API busca un recurso remoto sin validar la URI proporcionada por el usuario. Esto permite a un atacante forzar a la aplicación a enviar una solicitud manipulada a un destino inesperado, incluso cuando está protegido por un cortafuegos o una VPN.

Ejemplo Práctico:
Un atacante manipula una solicitud de API para incluir una URL remota maliciosa que apunta a un servidor interno. La API, sin validar adecuadamente la URI, realiza la solicitud y revela información confidencial o ejecuta acciones no autorizadas en el servidor interno.

Cómo Asegurarlo:
- Validar y filtrar adecuadamente las URI proporcionadas por los usuarios antes de enviar solicitudes a recursos remotos.
- Configurar listas blancas o negras de dominios y direcciones IP permitidas/restringidas para limitar los destinos posibles de las solicitudes.

## API8:2023 - Configuración de Seguridad Incorrecta (Security Misconfiguration)
Las APIs y los sistemas que las respaldan suelen tener configuraciones complejas para hacer que las APIs sean más personalizables. Los ingenieros de software y DevOps pueden pasar por alto estas configuraciones o no seguir las mejores prácticas de seguridad en cuanto a la configuración, abriendo la puerta a diferentes tipos de ataques.

Ejemplo Práctico:
Un API Gateway está mal configurado y permite el acceso no autorizado a los recursos de la API. Los endpoints confidenciales están expuestos públicamente debido a una mala configuración de las reglas de seguridad.

Cómo Asegurarlo:
- Realizar evaluaciones de seguridad regulares para identificar y corregir configuraciones incorrectas.
- Seguir las mejores prácticas de configuración de seguridad, como limitar los privilegios, deshabilitar funciones innecesarias y mantener las configuraciones actualizadas.

## API9:2023 - Gestión Inadecuada de Inventario (Improper Inventory Management)
Las APIs tienden a exponer más puntos finales que las aplicaciones web tradicionales, lo que hace que la documentación adecuada y actualizada sea muy importante. Un inventario adecuado de hosts y versiones de API implementadas también es importante para mitigar problemas como versiones de API obsoletas y puntos finales de depuración expuestos.

Ejemplo Práctico:
Un atacante descubre un punto final de API de depuración que revela información sensible y detalles de configuración. Esto puede ayudar al atacante a identificar vulnerabilidades y puntos débiles para futuros ataques.

Cómo Asegurarlo:
- Mantener una documentación completa y actualizada de la API, incluyendo los puntos finales expuestos y su funcionalidad.
- Realizar un seguimiento regular de los puntos finales implementados y eliminar o proteger adecuadamente los puntos finales de depuración o no utilizados.

## API10:2023 - Consumo No Seguro de APIs (Unsafe Consumption of APIs)
Los desarrolladores tienden a confiar más en los datos recibidos de APIs de terceros que en la entrada de los usuarios, y tienden a adoptar estándares de seguridad más débiles. Para comprometer las APIs, los atacantes se dirigen a los servicios de terceros integrados en lugar de intentar comprometer directamente la API objetivo.

Ejemplo Práctico:
Una aplicación confía ciegamente en la respuesta de una API de terceros para obtener datos sensibles. Un atacante intercepta la comunicación entre la aplicación y la API y modifica la respuesta para incluir datos maliciosos o manipulados.

Cómo Asegurarlo:
- Validar y filtrar cuidadosamente los datos recibidos de APIs de terceros.
- Aplicar mecanismos de seguridad adicionales, como firmas de mensajes o cifrado, para garantizar la integridad y autenticidad de los datos recibidos.
