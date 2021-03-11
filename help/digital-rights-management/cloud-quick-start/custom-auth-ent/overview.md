---
title: Información general sobre las abejas
description: Información general sobre las abejas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Información general sobre BEES{#bees-overview}

Puede implementar un servicio de derechos de back-end (BEES) para proporcionar derechos personalizados para su operación de DRM de Primetime Cloud.

Primetime Cloud DRM utiliza la entrega de licencias anónimas de forma predeterminada. Esto significa que todas las solicitudes de licencia enviadas a Primetime Cloud DRM devolverán una licencia válida sin realizar ninguna comprobación de autenticación/autorización adicional (a menos que haya aplicado una restricción de directiva que requiera utilizar la autenticación de Adobe Primetime).

La solicitud de licencia contiene la directiva DRM que se utilizó durante el empaquetado/encriptado del contenido. La directiva DRM se utiliza para generar la licencia DRM devuelta al cliente. En el escenario predeterminado, debe tomar todas las decisiones de directiva de DRM en el momento de empaquetar contenido. Los clientes que desean un control más preciso de estos flujos de trabajo tienen las siguientes opciones:

1. Integre la autenticación de Primetime para agregar comprobaciones de derechos adicionales antes de la reproducción.
1. Cree un servicio de asignación de derechos local al que Primetime Cloud DRM consultará antes de permitir que cualquier dispositivo reproduzca contenido que haya empaquetado.

El servicio de asignación de derechos local debe proporcionar una respuesta al DRM de Primetime Cloud que incluya los dos datos siguientes:

* `isAllowed`
* `drmPolicyToUse`

Estos factores determinan si un dispositivo puede reproducir el contenido y qué política de DRM utilizar para generar la licencia de DRM (si `isAllowed` es verdadera).

Este documento cubre lo que debe hacer para lograr la Opción 2 anterior: Implemente su propio servicio de asignación de derechos externo local y haga que esté disponible para Primetime Cloud DRM para el contenido que ha empaquetado.
