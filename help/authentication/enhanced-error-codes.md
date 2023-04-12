---
title: Códigos de error mejorados
description: Códigos de error mejorados
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# Códigos de error mejorados {#enhanced-error-codes}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview}

Este documento describe la lista de códigos de error de API y la información de error adicional devuelta a las aplicaciones.

Para utilizar los códigos de error mejorados en la aplicación Programadores, se debe realizar una solicitud al equipo de asistencia para habilitarlo con un cambio de configuración.

## Gestión de errores de respuesta {#response-error-handling}

En la mayoría de los casos, la API de autenticación de Primetime incluye información de error adicional en el cuerpo de la respuesta para proporcionar **contexto significativo** para saber por qué se ha producido un error determinado o soluciones posibles para remediar el problema automáticamente.  *Sin embargo, en algunos casos específicos que implican flujos de autenticación o cierre de sesión, los servicios de autenticación de Primetime podrían devolver una respuesta del HTML o un cuerpo vacío. Consulte la documentación de la API para obtener más información.*

Aunque ciertos tipos de errores se pueden controlar automáticamente (como volver a intentar una solicitud de autorización en caso de que se agote el tiempo de espera de la red o requerir que el usuario vuelva a autenticarse si su sesión ha caducado), otros tipos pueden requerir cambios de configuración o interacción con el equipo de atención al cliente. Es importante que los programadores recopilen y proporcionen información completa sobre los errores en estos casos.

La API de autenticación de Primetime devuelve códigos de estado HTTP en el rango 400-500 para indicar errores o errores. Cada código de estado HTTP tiene ciertas implicaciones:

- Los códigos de error 4xx implican que el error lo genera el cliente y que el cliente debe realizar un trabajo adicional para solucionarlo (por ejemplo, obtener un token de acceso antes de invocar API protegidas o proporcionar cualquier parámetro requerido)

- Los códigos de error 5xx implican que el servidor genera el error y que el servidor debe realizar un trabajo adicional para solucionarlo.

La información de error adicional se incluye en el campo &quot;error&quot; dentro del cuerpo de respuesta. 




| Nombre | Tipo | Ejemplo | Descripción |
| --- | --- | --- | --- |
| **error** | _object_ | JSON <br>    {<br>        &quot;status&quot; : 403,<br>        &quot;code&quot; : &quot;network_connection_failure&quot;,<br>        &quot;message&quot; : &quot;No se puede contactar con los servicios de su proveedor de TV&quot;,<br>        &quot;helpUrl&quot; : &quot;&quot;,<br>        &quot;trace&quot; : &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;acción&quot; : &quot;reintento&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | Una colección u objetos de error recopilados al intentar completar la solicitud. |

</br>

Las API de Adobe Primetime que administran varios elementos (API de preautorización, etc.) podrían indicar si el procesamiento de un elemento concreto ha fallado y si otros se ha realizado correctamente utilizando información de error de nivel de elemento. En este caso, la variable ***&quot;error&quot;*** El objeto se encuentra en el nivel de elemento y el cuerpo de respuesta puede contener varios ***&quot;errors&quot;*** objetos : consulte la documentación de la API.

</br>

| Ejemplo con éxito parcial y error de nivel de elemento |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; : &quot;TestStream1&quot;,<br>  &quot;authorized&quot; : true <br>}, </br>{ </br>  &quot;id&quot; : &quot;TestStream2&quot;, <br>   &quot;authorized&quot; : false, </br>   &quot;error&quot; : { <br> </br>      &quot;status&quot; : 403,<br>      &quot;code&quot; : &quot;network_connection_failure&quot;,<br>      &quot;message&quot; : &quot;No se puede contactar con los servicios de su proveedor de TV&quot;,<br>      &quot;detalles&quot; : &quot;&quot;,<br>      &quot;helpUrl&quot; : &quot;&quot;,<br>      &quot;trace&quot; : &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;acción&quot; : &quot;reintento&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

Cada objeto de error tiene los siguientes parámetros:

| Nombre | Tipo | Ejemplo | Restringido | Descripción |
|----|----|----|----|--------------|
| Estado | *integer* | 403 | ♦ | El código de estado HTTP de respuesta como se documenta en RFC 7231 (https://tools.ietf.org/html/rfc7231#section-6) <br> - 400 Solicitud incorrecta <br> - 400 Solicitud incorrecta <br> - 400 Solicitud incorrecta <br> - 401 No autorizado <br> - 403 Prohibido <br> - 404 No encontrado <br> - 405 Método no permitido <br> - 409 Conflicto <br> - 410 Atrás <br> - 412 Error en la precondición <br> - 429 Demasiadas solicitudes <br> - Error del servidor de intervalo 500 <br> - 503 Servicio no disponible |
| Código | *string* | network_connection_failure | ♦ | El código de error estándar de autenticación de Primetime. A continuación se incluye la lista completa de códigos de error. |
| message | *string* | No se puede contactar con los servicios del proveedor de TV |  | Mensaje legible por personas que se puede mostrar al usuario final. |
| detalles | *string* | El paquete de suscripción no incluye el canal &quot;Activo&quot; |  | En algunos casos, los extremos de autorización de MVPD o el programador proporcionan un mensaje detallado a través de las reglas de degradación. <br> <br> Tenga en cuenta que si no se recibió ningún mensaje personalizado de los servicios de socios, es posible que este campo no esté presente en los campos de error. |
| helpUrl | *url* | &quot;&quot; |  | Una URL que vincula a más información sobre por qué se produjo este error y posibles soluciones. <br> <br>  El URI representa una dirección URL absoluta y no debe deducirse del código de error. Según el contexto del error, se puede proporcionar una dirección URL diferente. Por ejemplo, el mismo código de error bad_request generará direcciones url diferentes para los servicios de autenticación y autorización. |
| trace | *string* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | Un identificador único para esta respuesta que se puede utilizar al ponerse en contacto con el servicio de asistencia para identificar problemas específicos en escenarios más complejos. |
| acción | *string* | reintento | ♦ | *Medidas recomendadas para remediar la situación:* </br><br> -none - Desafortunadamente no hay ninguna acción predefinida para remediar este problema. Esto podría indicar una invocación incorrecta de la API pública </br><br>-configuration : se necesita un cambio de configuración a través del panel TVE o poniéndose en contacto con el soporte técnico. </br><br>-application-registration - La aplicación debe registrarse de nuevo. </br><br>-authentication: el usuario debe autenticarse o volver a autenticarse. </br><br>-authorization: el usuario debe obtener autorización para el recurso específico. </br><br>-degradación - Debe aplicarse alguna forma de degradación. </br><br>-retry: si vuelve a intentar la solicitud, podría resolverse el problema</br><br>-retry-after - Reintentar la solicitud después del periodo de tiempo indicado podría resolver el problema. |

</br>

**Notas:**

- ***Restringido*** column *indica si el valor del campo correspondiente representa un conjunto finito* (por ejemplo, códigos de estado HTTP existentes para &quot;*status*&quot;). Las futuras actualizaciones de esta especificación podrían añadir valores a la lista restringida, pero no eliminarán ni cambiarán los existentes. Los campos sin restricciones generalmente pueden contener datos, pero puede haber limitaciones para garantizar un tamaño razonable.

- Cada respuesta de Adobe contendrá un &quot;Adobe-Solicitud-Id&quot; que identifica la solicitud del cliente en todos nuestros servicios HTTP. La variable **trace**&quot; complementa eso y deben informar juntos. 

## Códigos de estado HTTP y códigos de error {#http-status-codes-and-error-codes}

Las incoherencias entre los distintos códigos de error y sus códigos de estado HTTP asociados se deben a los requisitos de compatibilidad con versiones anteriores de los sdk y las aplicaciones ( por ejemplo *unknown\_application* genera 400 solicitudes incorrectas mientras *unknown\_software\_statement* rendimientos 401 (no autorizados). La solución de estas inconsistencias se dirigirá a futuras iteraciones. 
 
## Acciones y códigos de error {#actions-and-error-codes}

Para la mayoría de los códigos de error, se pueden elegir varias acciones como rutas para solucionar el problema o se pueden requerir incluso varias acciones para corregirlo automáticamente. Hemos elegido indicar el que tiene la mayor probabilidad de corregir el error. La variable **acciones** se puede dividir en tres categorías:

1. que intentan arreglar el contexto de solicitud (reintento, reintento después) 
1. que intentan arreglar el contexto de usuario dentro de la aplicación (registro de aplicación, autenticación, autorización) 
1. que intentan arreglar el contexto de integración entre una aplicación y un proveedor de identidad (configuración, degradación)

Para la primera categoría (reintento y después de reintento), simplemente reintentar la misma solicitud puede ser suficiente para resolver el problema. En casos de API que gestionen varios elementos, la aplicación debe repetir la solicitud e incluir solo aquellos elementos con una acción &quot;reintento&quot; o &quot;reintento después&quot;. Para &quot;*retry-after*&quot;, un &quot;<u>Reintentar después</u>&quot; indicará cuántos segundos debe esperar la aplicación antes de repetir la solicitud.

Para la segunda y tercera categoría, la implementación de la acción real depende en gran medida de las funciones de la aplicación. Por ejemplo, &quot;*degradación*&quot; puede implementarse como &quot;cambiar a 15 minutos de pases temporales para permitir a los usuarios la reproducción del contenido&quot; o como &quot;herramienta automática para aplicar la degradación AUTHN-ALL o AUTHZ-ALL para su integración con el MVPD especificado&quot;. Similar a &quot;*autenticación*&quot; puede déclencheur una autenticación pasiva (autenticación de canal posterior) en una tableta y un flujo de autenticación de 2ª pantalla completa en televisores conectados. Por eso optamos por proporcionar direcciones URL completas con esquema y todos los parámetros. 

## Códigos de error {#error-codes}

La siguiente tabla de errores muestra los posibles códigos de error, mensajes asociados y posibles acciones.

| Acción | Código de error | Código de estado HTTP | Descripción |
|---|---|---|--------------|
| configuración | *authorization_deny_by_mvpd* | 403 | La MVPD ha devuelto una decisión de &quot;Denegar&quot; al solicitar la autorización para el recurso especificado. |
|  | *authorization_deny_by_parent_controls* | 403 | El MVPD ha devuelto una decisión de &quot;Denegar&quot; debido a la configuración de controles parentales para el recurso especificado. |
|  | *authorization_deny_by_programmer* | 403 | La regla de degradación aplicada por el programador exige una decisión de &quot;Denegar&quot; para el usuario actual. |
|  | *bad_request* | 400 | La solicitud de API no es válida o está mal formada. Revise la documentación de la API para determinar los requisitos de la solicitud. |
|  | *individualization_service_available* | 503 | La solicitud falló debido a que el servicio de personalización no estaba disponible. |
|  | *internal_error* | 500 | La solicitud falló debido a un error interno del servidor. |
|  | *invalid_client_time* | 400 | La fecha/hora/zona horaria del equipo cliente no está configurada correctamente. Esto probablemente lleve a errores de autenticación/autorización. |
|  | *invalid_custom_scheme* | 400 | No se reconoce el esquema personalizado especificado que se usa en el registro de la aplicación. Compruebe la configuración del tablero TVE para ver los valores de esquema personalizados adecuados. |
|  | *invalid_domain* | 400 | El solicitante está utilizando un dominio no válido. Todos los dominios utilizados por un ID de solicitante en particular deben incluirse en la lista blanca de Adobes. |
|  | *invalid_header* | 400 | La solicitud falló porque contenía un encabezado no válido. Revise la documentación de la API para determinar qué encabezados son válidos para la solicitud y si hay limitaciones en su valor. |
|  | *invalid_http_method* | 405 | No se admite el método HTTP asociado a la solicitud. Revise la documentación de la API para determinar los métodos HTTP admitidos para la solicitud. |
|  | *invalid_parameter_value* | 400 | La solicitud ha fallado porque contenía un parámetro o valor de parámetro no válido. Revise la documentación de la API para determinar qué parámetros son válidos para su solicitud y si existen limitaciones para su valor. |
|  | *invalid_resource_value* | 400 | Error en la solicitud porque se utilizó un recurso no válido o de formato incorrecto. Revise la documentación de la API para determinar cómo se deben codificar los recursos complejos para la solicitud y si existen limitaciones en cuanto a su valor o tamaño. |
|  | *invalid_registration_code | 404 | El código de registro especificado ya no es válido o ha caducado. |
|  | *invalid_service_configuration* | 500 | Error en la solicitud debido a una configuración de servicio incorrecta. |
|  | *missing_authentication_header* | 400 | La solicitud ha fallado porque no contiene el encabezado de autenticación necesario para la API específica. |
|  | *missing_resource_mapping* | 400 | No hay ninguna asignación correspondiente para el recurso especificado. Póngase en contacto con el servicio de asistencia técnica para corregir la asignación necesaria. |
|  | *preauthorization_deny_by_mvpd* | 403 | El MVPD ha devuelto una decisión de &quot;Denegar&quot; al solicitar la preautorización para el recurso especificado. |
|  | *preauthorization_deny_by_programmer* | 403 | Las reglas de degradación aplicadas por el programador aplican una decisión de &quot;Denegar&quot; para el usuario actual. |
|  | *registration_code_service_available* | 503 | La solicitud falló porque el servicio de códigos de registro no está disponible. |
|  | *service_available | 503 | La solicitud ha fallado debido a que el servicio de autenticación o autorización no está disponible. |
|  | *access_token_available* | 400 | La solicitud falló debido a un error inesperado al recuperar el token de acceso. Compruebe la configuración del tablero TVE para ver si hay instrucciones de software disponibles y esquemas personalizados registrados. |
|  | *unsupported_client_version* | 400 | Esta versión del SDK de autenticación de Primetime es demasiado antigua y ya no es compatible. Consulte la documentación de la API para conocer los pasos necesarios para actualizar a la versión más reciente. |
|  | *network_required_ssl* | 403 | Hay un problema de conexión SSL para el servicio de socio de destino. Póngase en contacto con el equipo de asistencia técnica. |
|  | *too_many_resources* | 403 | Error en la solicitud de autorización o preautorización porque se consultaron demasiados recursos. Póngase en contacto con el equipo de asistencia para configurar correctamente las limitaciones de autorización y preautorización. |
|  | *unknown_programmer | 400 | No se reconoce el programador o el proveedor de servicios. Utilice el TVE Dashboard para registrar al programador especificado. |
|  | *unknown_application* | 400 | No se reconoce la aplicación. Utilice el panel de control de Televisión para registrar la aplicación especificada. |
|  | *unknown_integration* | 400 | La integración entre el programador especificado y el proveedor de identidad no existe. Utilice el panel de control de Televisión para crear la integración necesaria. |
|  | *unknown_software_statement* | 401 | No se reconoce la instrucción de software asociada al token de acceso. Póngase en contacto con el equipo de soporte técnico para aclarar el estado de la declaración del software. |
| aplicación-registro | *access_token_expire* | 401 | El token de acceso ha caducado. La aplicación debe actualizar el token de acceso como se indica en la documentación de la API. |
|  | *invalid_access_token_signature* | 401 | La firma del token de acceso ya no es válida. La aplicación debe actualizar el token de acceso como se indica en la documentación de la API. |
|  | *invalid_client_id* | 401 | No se reconoce el identificador de cliente asociado. La aplicación debe seguir el proceso de registro de la aplicación que se indica en la documentación de la API. |
| autenticación | *authentication_session_expire* | 410 | La sesión de autenticación actual ha caducado. El usuario debe volver a autenticarse con un MVPD compatible para poder continuar. |
|  | *authentication_session_missing* | 401 | No se pudo recuperar la sesión de autenticación asociada con esta solicitud. El usuario debe volver a autenticarse con un MVPD compatible para poder continuar. |
|  | *authentication_session_invalidated* | 401 | El proveedor de identidad invalidó la sesión de autenticación. El usuario debe volver a autenticarse con un MVPD compatible para poder continuar. |
|  | *authentication_session_issuer_mismatch | 400 | La solicitud de autorización falló debido al hecho de que el MVPD indicado para el flujo de autorización es diferente del que emitió la sesión de autenticación. El usuario debe volver a autenticarse con el MVPD deseado para poder continuar. |
|  | *authorization_deny_by_hba_policy* | 403 | El MVPD ha devuelto una decisión de &quot;Denegar&quot; debido a políticas de autenticación basadas en el hogar. La autenticación actual se obtuvo mediante un flujo de autenticación basado en el hogar (HBA), pero el dispositivo ya no está en casa al solicitar la autorización para el recurso especificado. El usuario debe volver a autenticarse con un MVPD compatible para poder continuar. |
|  | *identity_not_known_by_mvpd* | 403 | La solicitud de autorización falló debido al hecho de que la MVPD no reconoció la identidad del usuario. |
| autorización | *authorization_expire* | 410 | La autorización anterior para el recurso especificado ha caducado. El usuario debe obtener una nueva autorización para continuar. |
|  | *authorization_not_found* | 404 | No se encontró ninguna autorización para el recurso especificado. El usuario debe obtener una nueva autorización para continuar. |
|  | *device_identifier_mismatch* | 403 | El identificador de dispositivo especificado no coincide con la identificación del dispositivo de autorización. El usuario debe obtener una nueva autorización para continuar. |
| reintento | **network_connection_failure** | 403 | Error de conexión con el servicio asociado. Volver a intentar la solicitud podría resolver el problema. |
|  | *network_connection_timeout* | 403 | Se agotó el tiempo de espera de conexión con el servicio asociado. Volver a intentar la solicitud podría resolver el problema. |
|  | *network_received_error* | 403 | Error de lectura al recuperar la respuesta del servicio asociado. Volver a intentar la solicitud podría resolver el problema. |
|  | *maximum_execution_time_expanded* | 403 | La solicitud no se completó en el tiempo máximo permitido. Volver a intentar la solicitud podría resolver el problema. |
| retry-after | *too_many_request* | 429 | Se han enviado demasiadas solicitudes dentro de un intervalo determinado. La aplicación puede reintentar la solicitud después del periodo de tiempo sugerido. |
|  | *user_rate_limit_expanded* | 429 | Un usuario en particular ha emitido demasiadas solicitudes dentro de un intervalo determinado. La aplicación puede reintentar la solicitud después del periodo de tiempo sugerido. |

