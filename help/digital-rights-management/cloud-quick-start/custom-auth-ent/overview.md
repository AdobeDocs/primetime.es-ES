---
title: Información general sobre ABEJAS
description: Información general sobre ABEJAS
copied-description: true
exl-id: 481af72b-40a3-4f33-9e91-990dc5308596
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Información general sobre ABEJAS{#bees-overview}

Puede implementar un Servicio de derechos de back-end (BEES) para proporcionar derechos personalizados para su operación de DRM de Primetime Cloud.

Primetime Cloud DRM utiliza la entrega de licencias anónimas de forma predeterminada. Esto significa que todas las solicitudes de licencia enviadas a Primetime Cloud DRM devolverán una licencia válida sin realizar ninguna comprobación de autenticación/autorización adicional (a menos que haya aplicado una restricción de directiva que requiera el uso de la autenticación de Adobe Primetime).

La solicitud de licencia contiene la política DRM que se utilizó durante el empaquetado/cifrado del contenido. La directiva DRM se utiliza para generar la licencia DRM devuelta al cliente. En el escenario predeterminado, debe tomar todas las decisiones de política de DRM en el momento del empaquetado del contenido. Los clientes que desean un control más preciso sobre estos flujos de trabajo tienen las siguientes opciones:

1. Integre la autenticación de Primetime para añadir comprobaciones de derechos adicionales antes de la reproducción.
1. Cree un servicio de asignación de derechos local que Primetime Cloud DRM consultará antes de permitir que cualquier dispositivo reproduzca contenido que haya empaquetado.

El servicio de asignación de derechos local debe proporcionar una respuesta a Primetime Cloud DRM que incluya los dos datos siguientes:

* `isAllowed`
* `drmPolicyToUse`

Estos determinan si se permite a un dispositivo reproducir el contenido y qué política de DRM utilizar para generar la licencia de DRM (si `isAllowed` es true).

Este documento explica lo que debe hacer para lograr la opción 2 anterior: Implementar su propio servicio de asignación de derechos externo local y ponerlo a disposición de Primetime Cloud DRM para el contenido que ha empaquetado.
