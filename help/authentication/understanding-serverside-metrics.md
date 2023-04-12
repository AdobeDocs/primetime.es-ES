---
title: Explicación de las métricas del lado del servidor
description: Explicación de las métricas del lado del servidor
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---

# Explicación de las métricas del lado del servidor {#understanding-server-side-metrics}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Introducción {#intro}

Este documento describe las métricas del lado del servidor de autenticación de Adobe Primetime generadas por el servicio de supervisión del servicio de derechos (ESM). No describe los mismos eventos que se ven desde la perspectiva del lado del cliente (lo que los programadores verían si implementaran un servicio de medición como Adobe Analytics en su página/aplicación).  

## Resumen de eventos {#events_summary}

Desde el punto de vista del servidor de autenticación de Adobe Primetime, se generan los siguientes eventos:

* **Eventos generados en el flujo de autenticación**(Un inicio de sesión real con el MVPD)

   * Notificación de intento de AuthN : esto se genera cuando el usuario se envía al sitio de inicio de sesión de MVPD.
   * Notificación de AuthN pendiente : si el usuario logra iniciar sesión con su MVPD, esto se genera cuando se redirige al usuario de nuevo a la autenticación de Primetime.
   * Notificación de autenticación concedida : esto se genera cuando el usuario vuelve al sitio del programador y ha recuperado correctamente el token de autenticación de la autenticación de Primetime. 
* **Flujo de autorización** (Sólo una comprobación de autorización con un MVPD)\
   *Requisito previo:* Un token AuthN válido
   * Notificación del intento de AuthZ
   * Notificación de AuthZ concedida
* **Solicitud de reproducción correcta**\
   *Requisito previo:* Tokens válidos de AuthN y AuthZ
   * Notificación de una comprobación con autenticación de Adobe Primetime 
   * Una solicitud de reproducción requiere tanto una autenticación concedida como una autorización concedida


El número de usuarios únicos se explica detalladamente en la [Usuarios únicos](#unique-users) a continuación. Como información general, dado que las respuestas de autenticación y autorización concedidas generalmente se almacenan en caché, se aplican las siguientes fórmulas:

* Número de intentos de AuthN \> Número de intentos de AuthN concedidos
* Número de intentos de AuthZ \> Número de intentos de AuthZ concedidos
* Número de intentos de AuthZ \> Número de intentos de AuthN concedidos (normalmente)
* Número de solicitudes de reproducción correctas \> Número de AuthZ concedidas


### Ejemplo {#example}

En el siguiente ejemplo se muestran las métricas del lado del servidor correspondientes a un mes para una marca:

| Métrica | MVPD 1 | MVPD 2 | ... | MVPD n | Total | | — | — | — | - | — | — | | Autenticaciones correctas | 1125 | 2892 | | 2203 | SUM(MVP1+...MVPD n) | | Autorizaciones correctas | 2527 | 5603 | | 5904 | SUM(MVP1+...MVPD n) | | Solicitudes de reproducción correctas | 4201 | 10518 | | 10737 | SUM(MVP1+...MVPD n) | | Usuarios únicos | 1375 | 2400 | | 2890 | SUMA de todos los usuarios para todos los MVPD deduplicados\* | | Autenticaciones intentadas | 2147 | 3887 | | 3108 | SUM(MVP1+...MVPD n) | | Intento de autorización | 2889 | 6139 | | 6039 | SUM(MVP1+...MVPD n) |

</br>

En este caso, la deduplicación no debería tener ningún efecto, ya que los distintos usuarios de MVPD no deberían recibir el mismo ID de usuario. Al hacer una suma para dos marcas diferentes pero el mismo MVPD, el efecto de deduplicación debería ser mucho mayor.

## Déclencheur de eventos {#event_triggers}

### Nuevo usuario: flujo completo {#new-user-full-flow}

En el gráfico siguiente se describen los eventos y pasos de un usuario sin token de autenticación (un usuario nuevo o un token de autenticación de usuario que ha caducado):



![](assets/ae-flow-with-events.png)



El flujo implica viajes de ida y vuelta a los MVPD tanto para la autenticación (#5 a \#7) como para la autorización (\#11).



Una vez completado el flujo, los tokens de autenticación y autorización se almacenan en caché en el dispositivo del usuario. Los valores de tiempo de vida (TTL) de los tokens de autenticación están entre 6 y 90 días. Una caducidad de token AuthN fuerza automáticamente una caducidad de token AuthZ. El valor TTL del token de autorización suele ser de 24 horas.

| Eventos del lado del servidor activados | <ul><li>Intento de autenticación, Autenticación pendiente, Autenticación concedida</li><li>Intento de autorización, autorización concedida</li><li>Solicitud de reproducción correcta</li></ul> |
|---|---|


### Usuario que regresa: Tokens AuthZ y AuthN en caché

Para los usuarios que tienen tokens AuthZ y AuthN válidos en la caché, se dan los siguientes pasos:


![](assets/ae-flow-tokens-cached-web.png)



Esto se activa automáticamente al llamar a `getAuthorization()`, y solo incluye comprobaciones con autenticación de Adobe Primetime. El MVPD no participa en este flujo.


| Eventos del lado del servidor activados | * Solicitud de reproducción correcta |
|---|---|


### Usuario que regresa: Tokens de AuthN en la caché, token de AuthZ caducado

Para los usuarios que aún tienen tokens de AuthN válidos, se dan los siguientes pasos:

![](assets/ae-flow-authn-token-cached.png)


Este flujo implica un viaje de ida y vuelta al MVPD.


| Eventos del lado del servidor activados | <ul><li>Intento de autorización, autorización correcta</li><li>Solicitud de reproducción correcta</li> |
|---|---|

## Eventos de autenticación {#authn_events}

### Intento de autenticación {#authentication-attempt}

Como se ilustra en el diagrama anterior, los eventos de autenticación solo se activan cuando el usuario realiza un viaje de ida y vuelta al MVPD; los eventos de autenticación no incluyen autenticaciones de token en caché.

El evento de intento de autenticación se activa después de que el usuario haya hecho clic en un MVPD concreto desde el selector.

* El primer evento del lado MVPD que está cerca de esto es la carga de la página
* La autenticación de Adobe Primetime no cuenta los repetidos intentos del usuario de iniciar sesión en la página MVPD (contraseña incorrecta, inténtelo de nuevo)
* varios intentos se cuentan como un solo intento
* Algunos MVPD también realizan la Autorización en el paso Autenticación y el usuario no es redirigido si la autorización falla.

### Autenticación pendiente {#authentication-pending}

Este evento se produce cuando se inicia el proceso de redireccionamiento a la autenticación de Adobe Primetime.

### Autenticación concedida {#authentication-granted}

El usuario es un suscriptor conocido del MVPD, normalmente con una suscripción de televisión de pago, pero a veces solo con acceso a Internet. Puede producirse una autenticación correcta ya sea porque el usuario introdujo explícitamente credenciales válidas con su MVPD, o porque previamente había introducido credenciales válidas y había marcado &quot;Recordarme&quot; (y la sesión anterior no había caducado).

Por lo tanto, el MVPD envía a la autenticación de Adobe Primetime una respuesta positiva a la solicitud de autenticación y la autenticación de Adobe Primetime crea un *Token AuthN*.

* La autenticación generalmente se almacena en caché durante un largo período de tiempo (un mes o más). Debido a esto, los eventos de autenticación ya no estarán presentes hasta que el token caduque y se reinicie el flujo.
* La entrada desde otro sitio o aplicación a través del inicio de sesión único no déclencheur los eventos de autenticación.

 

### Autenticación mediante transmisión {#comcast-authentication}

Comcast tiene un flujo AuthN diferente comparado con el resto de los MVPD.

Las siguientes características describen las diferencias:

* **Comportamiento de la cookie de sesión**: Esto provoca la eliminación completa de todos los tokens de autenticación después de que el usuario haya cerrado el explorador. Esta función solo está presente en la web. El objetivo principal es garantizar que la sesión de Comcast no se mantenga en equipos no seguros o compartidos. El impacto es que habrá más intentos de autenticación / flujos concedidos que para el resto de los MVPD.

* **AuthN por requestorID**: Comcast no permite que el estado AuthN se almacene en caché de un ID de solicitante a otro. Debido a esto, cada sitio /aplicación tiene que ir a Comcast para obtener un token de autenticación. Además de las consideraciones de experiencia del usuario, el impacto, como se ha indicado anteriormente, es que se generarán más intentos de autenticación/eventos concedidos.

* **Autenticación pasiva**: Para mejorar la experiencia del usuario pero mantener la funcionalidad AuthN per requestorID , se produce un flujo de autenticación pasivo en un iFrame oculto. El usuario no verá nada excepto que los eventos se activarán como antes.

Si el usuario hace clic en &quot;recordarme&quot; en la página de inicio de sesión de Comcast, las posteriores visitas a esta página (en un período de 2 semanas) serán solo una redirección rápida. De lo contrario, los usuarios tendrán que autenticarse en la página.

### Autenticación incorrecta {#unsuccessful-authentication}

Una autenticación incorrecta no es un evento per se en la autenticación de Adobe Primetime, pero se puede calcular como la diferencia entre intentos y éxitos.

En la versión de mayo de 2013, la autenticación de Adobe Primetime agregará códigos de error para autenticaciones fallidas debidas a errores de sistema o de red, incluidos errores de DRM (error de enlace de tokens) y errores de LSO (sin espacio para escribir el token, etc.).

### Tasa de conversión de autenticación {#authenitication-conversion-rate}

Una métrica interesante que los programadores pueden rastrear es la tasa de conversión de autenticación, calculada como (solicitudes AuthN / AuthN concedido)%.

Algunas notas sobre las métricas:

* Como es una métrica basada en eventos, no refleja realmente la tasa de conversión de usuario único (si un usuario lo intenta ocho veces y lo consigue por novena vez), esto se reflejará muy mal en la tasa de conversión anterior.
* No hay forma (todavía) en la autenticación de Adobe Primetime (en el lado del servidor) de calcular una conversión de autenticación basada en única.
* Si hay reintentos automáticos de AuthN presentes en el sitio o la aplicación, también se distorsionará la métrica anterior.

## Eventos de autorización {#authorization_events}

### Intento de autorización {#authorization_attempt}

Además de obtener un token de autenticación, los usuarios también deben obtener un token de autorización antes de reproducir el contenido. Esto suele ocurrir después de la autenticación o si el token de autorización caduca. Dado que esta comprobación se realiza en el lado del servidor (desde los servidores de autenticación de Adobe Primetime hasta los servidores MVPD), el usuario no tiene que hacer nada.

### Autorización concedida {#authorization-granted}

Una &quot;autorización concedida&quot; indica que la suscripción del usuario autenticado incluye la programación solicitada.

Tenga en cuenta que no todos los MVPD admiten un paso de autorización separado; para cierta autenticación se equipara con autorización. El MVPD envía a la autenticación de Adobe Primetime una respuesta correcta a la solicitud AuthZ del canal inverso y la autenticación de Adobe Primetime crea un token AuthZ.

* El token AuthZ se almacena en caché durante un período de tiempo, normalmente 24 horas Durante este período no se activarán eventos AuthZ.
* Algunos MVPD trabajan con autorizaciones de nivel de recursos, otros con autorizaciones de nivel de canal; - dependiendo de cuál se use, se activan más o menos eventos AuthZ. Incluso para la autorización de nivel de canal, el almacenamiento en caché está en su lugar, por lo que si el mismo recurso se solicita en menos de 24 horas, no se activará ningún evento.

### Autorización denegada {#authorization-denied}

Si se deniega una autorización, el usuario autenticado no tiene una suscripción confirmada a la programación solicitada. La causa más probable es que el canal no forme parte del paquete de suscripción del usuario, pero esto también puede reflejar a un usuario que solo tiene acceso a Internet desde el MVPD.

Para algunos MVPD, los usuarios se autentican correctamente aunque solo tengan una suscripción a Internet de MVPD (sin suscripción a televisión de pago). En este caso, aunque el canal para el que el usuario solicita la autorización esté en el paquete base, la autorización se deniega.

Algunos MVPD ofrecen mensajes de error personalizados para denegaciones de AuthZ que pueden incluir ofertas para actualizar su paquete.


### Tasa de conversión de autorización {#authorization-conversion-rate}

La tasa de conversión de autenticación se puede calcular como (solicitudes AuthZ / AuthZ concedido)%.

### Solicitud de reproducción correcta {#successful-play-request}

Un usuario autenticado y autorizado puede ver el contenido protegido.

Cuando la solicitud de reproducción se realiza correctamente, la autenticación de Adobe Primetime genera un token de medios de duración corta que afirma que el usuario tiene derecho a ver el vídeo solicitado. El programador utiliza este token multimedia para validar aún más el visor potencial. Los tokens de medios se rastrean como solicitudes de reproducción correctas.

* La autenticación de Adobe Primetime sí *not* realice un seguimiento de si la reproducción de vídeo comenzó después de generar el token de medios. Por ejemplo, si hay una restricción geográfica en el contenido, la transacción sigue contando como una solicitud de reproducción correcta, aunque la emisión nunca se inicie.
* Dado que los tokens AuthN y AuthZ almacenan en caché la respuesta de MVPD durante un periodo de tiempo, el evento de solicitud de reproducción exitoso es el evento más frecuente en las métricas.

## Usuarios únicos {#unique-users}

### Definición {#definition}

Tras una autenticación correcta, la autenticación de Adobe Primetime rastrea la existencia de un usuario único, en función del valor de ID de usuario MVPD devuelto.  Este valor se basa en la información de inicio de sesión del usuario, pero no contiene información de identificación personal.

Este valor también se pasa al sitio o aplicación en la llamada de retorno sendTrackingData .

Este valor puede ser persistente entre dispositivos (el MVPD produce el mismo valor para un usuario determinado, independientemente de dónde se produzca el inicio de sesión) o transitorio (para cada inicio de sesión, se genera un nuevo valor, que el MVPD asigna en su back-end. Normalmente, los valores proporcionados por los MVPD para la autenticación de Adobe Primetime son persistentes entre sesiones y dispositivos, pero, como se ha señalado, la persistencia no está garantizada ni validada.

Este valor se utiliza como una forma de calcular los usuarios únicos. El valor registrado (por ID/intervalo/MVPD del solicitante) se deduplica para el intervalo en particular. Por lo tanto, la suma de los usuarios únicos por día suele ser diferente al valor mensual, con el valor mensual que tiene el menor valor.

Este número incluye todos los eventos de autenticación de Adobe Primetime, menos los intentos de autenticación (que no tienen ID de usuario), pero incluidas las autorizaciones intentadas (y posiblemente fallidas).

### Ejemplos {#examples}

#### Día 1 {#day1}

El usuario XYZ va al sitio para ver un vídeo.

Eventos activados:

* Intento de AuthN (aún no es un usuario único)
* AuthN concedido
   * en este punto identificamos de forma exclusiva al usuario en función de lo que devuelve el MVPD, de modo que el recuento diario de usuarios únicos aumenta en 1
   * el token AuthN se almacena en caché durante 30 días
* Intento de AuthZ/evento concedido
   * Token de AuthZ almacenado en caché durante 1 día
* Evento de solicitud de reproducción correcta

#### Día 1 (posterior) {#day1-later-on}

El usuario XYZ ve otro vídeo.

Eventos activados:

* Evento de solicitud de reproducción correcta (el resto se almacena en caché)
* Sin aumento de valores únicos diarios o mensuales

#### Día 3 {#day3}

El usuario XYZ ve otro vídeo.

Eventos activados:

* Intento de AuthZ/evento concedido
   * Desde 1 día de almacenamiento en caché desde el día 1 ha caducado
* Evento de solicitud de reproducción correcta (el resto se almacena en caché)
* Usuarios únicos diarios aumentados en 1: los únicos mensuales siguen siendo 1

#### Día 31 {#day31}

El usuario XYZ ve otro vídeo.

Igual que en el día 1 desde que caducó el almacenamiento en caché de AuthN.

Si el mismo usuario fallara en la autorización, el recuento de usuarios únicos mensuales seguiría aumentando en 1 porque hay dos eventos que contienen el ID de usuario (autenticación concedida y intento de autorización).

### Inicio de sesión único (SSO) {#single-sign-on-sso}

En algunos casos, el número de usuarios únicos puede ser mayor que el número de autenticaciones correctas. Este suele ser el caso cuando muchos usuarios llegan a través de SSO desde otros sitios/aplicaciones, y solo necesitan obtener autorización en el sitio/aplicación actual.

### Comparación de usuarios únicos del lado del cliente y del lado del servidor {#comparing-client-side-and-server-side-unique-users}

Si el valor de ID de usuario de `sendTrackingData()` se usa en el lado del cliente para contar usuarios únicos, entonces los números del lado del cliente y del lado del servidor deben coincidir.

Si las diferencias son mayores, las siguientes razones suelen explicar la diferencia:

* Los únicos de reproducción de vídeo frente a todos los eventos únicos. Como se ha mencionado, la autenticación de Adobe Primetime cuenta usuarios únicos para todos los eventos excepto para los intentos de AuthN. Esto significa que si el usuario solo se autentica (en la página) pero no ve un vídeo, se sigue activando un aumento en el recuento de usuarios únicos.

* Recuento de usuarios con errores de autorización: la autenticación de Adobe Primetime cuenta también a estos usuarios en el número registrado.

<!--
## Related Information {#related-information}

- [Entitlement Service Monitoring API](/help/authentication/entitlement-service-monitoring-api.md)

-->