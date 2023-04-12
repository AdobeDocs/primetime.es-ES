---
title: Información general sobre la supervisión del servicio de derechos
description: Información general sobre la supervisión del servicio de derechos
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Información general sobre la supervisión del servicio de derechos {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#introduction}

Los sitios y aplicaciones de TVE deben estar disponibles las 24 horas del día, los 7 días de la semana, por lo que los clientes necesitan una perspectiva en tiempo real de los eventos de asignación de derechos para detectar y corregir problemas lo antes posible. También deben analizar los datos mensuales para determinar qué plataformas proporcionan la mayor parte del tráfico y qué plataformas pueden tener una implementación incorrecta y tasas de conversión deficientes.

La supervisión del servicio de derechos (ESM) proporciona a los programadores y a los MVPD una fuente de datos que ofrece visibilidad en tiempo real de sus eventos de autenticación y autorización. Los datos se recopilan desde los sistemas de autenticación de Adobe Primetime y se proporcionan a través de una API de RESTful.  Los clientes pueden consumir los datos de forma directa o desde sus propios paneles operativos personalizados.

Los elementos centrales del sistema ESM son sus métricas y dimensiones. ESM genera informes que contienen métricas agregadas según la selección de dimensiones. Como los eventos de Adobe Pass se registran en la zona horaria de PST, los informes de ESM también están disponibles en la zona horaria de PST. 

La API de ESM no está disponible de forma general.  Póngase en contacto con su representante de Adobe para obtener más información sobre la disponibilidad.

## ESM para programadores {#esm-for-programmers}

### Los programadores pueden monitorizar las siguientes métricas: {#programmers-monitor-metrics}


| *Nombre de las métricas* | *Descripción* |
|-------------------------|--------------------------|
| authn-intentos | Número de flujos de autenticación iniciados |
| authn-success | Número de tokens de autenticación obtenidos correctamente por clientes |
| authn-pending | Número de tokens de autenticación generados correctamente (sin tener en cuenta si el cliente lo obtuvo o no) |
| authn-failed | Número de autenticación fallida realizada a través de un sistema externo. |
| clientless-tokens | Número de tokens sin cliente emitidos correctamente |
| clientless-failure | Número de intentos fallidos de recibir tokens desde la API sin cliente |
| authz-intentos | Número de autorizaciones intentadas |
| authz-success | Número de autorizaciones correctas |
| authz-failed | Número de autorizaciones denegadas por MVPD a nivel de aplicación |
| authz-rejected | Número de intentos de autorizaciones que el proveedor de servicios de Adobe considera maliciosos y que se rechazan como resultado de una prevención de ataques de DoS |
| authz-latency | Número total de milisegundos empleados en el punto final del MVPD |
| media-tokens | Número de tokens de medios cortos generados (que se asimilan al número de solicitudes de reproducción) |
| cuentas únicas | Número de usuarios únicos que realizaron acciones de asignación de derechos (AuthN / AuthZ) en el intervalo de tiempo seleccionado. (Esta métrica solo se mostrará si se solicitan valores diarios). </br> Esto se calcula para cada centro de datos individual. Cuando no se solicita la dimensión &quot;dc&quot;, esta métrica no se muestra. |
| sesiones únicas | Número de sesiones únicas que realizaron llamadas de flujo de autenticación al servicio de autenticación de Adobe Primetime dentro del intervalo de tiempo seleccionado. (Esta métrica solo se mostrará si se solicitan valores diarios). </br> Esto se calcula para cada centro de datos individual. Cuando no se solicita la dimensión &quot;dc&quot;, esta métrica no se muestra. |
| count | Un contador simple utilizado en los informes orientados a eventos |

</br>

### Los programadores pueden filtrar las métricas enumeradas arriba por las siguientes dimensiones: {#progr-filter-metrics}


| *Nombre del Dimension* | *Descripción* |
|---|---|
| año | El año de 4 dígitos |
| mes | Mes del año (1-12) |
| day | El día del mes (1-31) |
| hour | La hora del día |
| minuto | El minuto de la hora |
| media-company | Empresa de medios propietaria del sitio web que inició el proceso de asignación de derechos para el usuario |
| dc | (Centro de datos) Región de origen en la que se recibió la solicitud. |
| proxy | El MVPD proxy (que será &quot;directo&quot; para integraciones directas) |
| mvpd | El MVPD responsable de conceder el derecho al usuario |
| requestor-id | El ID del solicitante utilizado para realizar la solicitud de asignación de derechos |
| canal | El sitio web del canal, extraído del campo de recurso (extraído de la carga útil MRSS como canal/título si se proporciona, o asignado al valor del recurso si no está en formato RSS). |
| resource-id | El título real del recurso que participa en la solicitud de autorización (extraído de la carga útil MRSS como elemento/título, si se proporciona) |
| dispositivo | La plataforma del dispositivo (PC, móvil, consola, etc.) |
| eap | El proveedor de autenticación externa cuando el flujo de autenticación se realiza a través de un sistema externo. </br> Los valores pueden ser: </br> - N/D: la autenticación la proporcionó la autenticación Primetime </br> - Apple: el sistema externo que proporcionó la autenticación es Apple |
| os-family | Sistema operativo que se ejecuta en el dispositivo |
| browser-family | Agente de usuario utilizado para acceder a la autenticación de Adobe Primetime |
| cdt | La plataforma del dispositivo (alternativa), que actualmente se utiliza para Clientless. </br>  Los valores pueden ser: </br> - N/D: el evento no se originó en un SDK sin cliente </br> - Desconocido : como el parámetro deviceType de una API sin cliente es opcional, hay llamadas que no contienen ningún valor. </br> - cualquier otro valor que se haya enviado a través de la API sin cliente, por ejemplo, xbox, appletv, roku, etc. </br> |
| platform-version | La versión del SDK sin cliente |
| os-type | Sistema operativo que se ejecuta en el dispositivo, alternativo (no se utiliza actualmente) |
| browser-version | Versión del agente de usuario |
| tipo sdk | El SDK de cliente utilizado (Flash, HTML5, Android nativo, iOS, Clientless, etc.) |
| sdk-version | La versión del SDK del cliente de autenticación de Adobe Primetime |
| evento | El nombre del evento de autenticación de Adobe Primetime |
| reason | El motivo de los errores, tal como indica la autenticación de Adobe Primetime |
| sso-type | El mecanismo de SSO subyacente: platform/passive/adobe. Indica que el token de autorización se emitió reutilizando la AuthN en una aplicación diferente |

## ESM para MVPD {#esm-for-mvpds}

### Los MVPD pueden monitorizar las siguientes métricas:

| *Nombre de la métrica* | *Descripción* |
|---|---|
| authn-intentos | Número de flujos de autenticación iniciados |
| authn-success | Número de tokens de autenticación obtenidos correctamente por clientes |
| authn-pending | Número de tokens de autenticación generados correctamente (sin tener en cuenta si el cliente lo obtuvo o no) |
| authn-failed | Número de autenticación fallida realizada a través de un sistema externo. |
| authz-intentos | Número de autorizaciones intentadas |
| authz-success | Número de autorizaciones correctas |
| authz-failed | Número de autorizaciones denegadas por MVPD a nivel de aplicación |
| authz-rejected | Número de intentos de autorizaciones que el proveedor de servicios de Adobe considera maliciosos y que se rechazan como resultado de una prevención de ataques de DoS |
| authz-latency | Número total de milisegundos empleados en el punto final del MVPD |

### Los MVPD pueden filtrar las métricas enumeradas anteriormente por las siguientes dimensiones:

| *Nombre del Dimension* | *Descripción* |
|---|---|
| año | El año de 4 dígitos |
| mes | Mes del año (1-12) |
| day | El día del mes (1-31) |
| hour | La hora del día |
| minuto | El minuto de la hora |
| requestor-id | El ID del solicitante utilizado para realizar la solicitud de asignación de derechos |
| eap | El proveedor de autenticación externa cuando el flujo de autenticación se realiza a través de un sistema externo. </br> Los valores pueden ser: </br> - N/D: la autenticación la proporcionó la autenticación Primetime </br> - Apple: el sistema externo que proporcionó la autenticación es Apple |
| cdt | La plataforma del dispositivo (alternativa), que actualmente se utiliza para Clientless. </br>  Los valores pueden ser: </br> - N/D: el evento no se originó en un SDK sin cliente </br> - Desconocido : como el parámetro deviceType de una API sin cliente es opcional, hay llamadas que no contienen ningún valor. </br> - cualquier otro valor que se haya enviado a través de la API sin cliente, por ejemplo, xbox, appletv, roku, etc. </br> |
| tipo sdk | El SDK de cliente utilizado (Flash, HTML5, Android nativo, iOS, Clientless, etc.) |


## Casos de uso {#use-cases}

Puede utilizar los datos de ESM para los siguientes casos de uso:

- **Monitorización** : Los equipos de operaciones o de supervisión pueden crear un tablero o un gráfico que llame a la API cada minuto. Utilizando la información mostrada pueden detectar un problema (con autenticación de Primetime o con un MVPD) en el momento en que aparece.  

- **Depuración/Prueba de calidad** - Dado que los datos también se desglosan por plataforma, dispositivo, navegador y sistema operativo, el análisis de los patrones de uso puede identificar problemas en combinaciones específicas (por ejemplo, Safari en OSX).  

- **Analytics** : los datos proporcionados pueden utilizarse para complementar o auditar los datos del lado del cliente que se recopilan a través de Adobe Analytics u otra herramienta de análisis.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->