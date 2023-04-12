---
title: Información general de la API de degradación
description: Información general de la API de degradación
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Información general de la API de degradación {#degradation-api-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#general_info}

>[!NOTE]
>
>Esta API no está disponible en general. Póngase en contacto con su representante de Adobe para obtener actualizaciones de disponibilidad.

Esta función proporciona a cualquiera de las tres partes principales de una integración (programadores, MVPD y Adobe) la capacidad de evitar temporalmente puntos finales específicos de autenticación y autorización de MVPD. Normalmente es el Programador el que inicia tal acción, pero independientemente de quién déclencheur un evento de degradación, la acción depende de acuerdos previamente acordados con los MVPD afectados.

El caso de uso principal de esta función se produce durante deportes en directo o eventos grandes. En estos escenarios de alto tráfico es posible que la carga en un punto final específico de MVPD sea demasiado alta, lo que resulta en tiempos de respuesta muy largos para los usuarios. Para preservar una buena experiencia de usuario durante un escenario de este tipo, el programador puede decidir el déclencheur de una regla de degradación que pueda autenticar automáticamente o autorizar automáticamente temporalmente a los usuarios, o deshabilitar un MVPD eliminándolo de la lista de MVPD disponibles.

Una regla de degradación solo se aplica durante un período de tiempo fijo. Aunque los clientes principales de esta función son los canales deportivos y los canales de noticias en directo, es posible que cualquier programador desee tener acceso a esta función, ya que los servicios de MVPD se reducen de vez en cuando.

Notas de degradación:

* Esta función está diseñada para utilizarse junto con la API de supervisión del uso, que proporciona información en tiempo real sobre el número de autenticaciones y autorizaciones por MVPD, la latencia media de autorización y otras métricas necesarias para obtener una descripción general completa del servicio.
* Esta función no permite evitar el servicio de autenticación de Adobe Primetim. Si la autenticación de Primetime no está disponible, no hay ningún mecanismo dentro del servicio que pueda utilizarse para permitir a los usuarios ver el contenido. Sin embargo, los sitios o aplicaciones pueden enrutar por sí mismos la autenticación de Primetime.
* Actualmente, el Adobe no degradará directamente el déclencheur: la decisión siempre debe residir con un programador específico que haya aceptado tales condiciones con los MVPD. En el futuro, la autenticación de Primetime podría ser proactiva a la hora de activar las reglas de degradación si se pueden alcanzar acuerdos (protección del SLA) con MVPD.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->