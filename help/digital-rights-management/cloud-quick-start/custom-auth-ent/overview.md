---
seo-title: INFORME DE ABEJAS
title: INFORME DE ABEJAS
uuid: c6ee7528-fdfa-4a56-bea2-a5e2dab6d428
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Información general sobre las BEES{#bees-overview}

Puede implementar un servicio de asignación de derechos de back-end (BEES) para proporcionar asignación de derechos personalizada para su operación de DRM de Primetime Cloud.

Primetime Cloud DRM utiliza envío de licencia anónimo de forma predeterminada. Esto significa que todas las solicitudes de licencia enviadas a Primetime Cloud DRM devolverán una licencia válida sin realizar ninguna comprobación de autenticación o autorización adicional (a menos que haya aplicado una restricción de directiva que requiera el uso de la autenticación de Adobe Primetime).

La solicitud de licencia contiene la directiva DRM que se utilizó durante el empaquetado/cifrado del contenido. La directiva DRM se utiliza para generar la licencia de DRM devuelta al cliente. En el escenario predeterminado, debe tomar todas las decisiones de directiva DRM en el momento del empaquetado de contenido. Los clientes que desean un control más preciso sobre estos flujos de trabajo tienen las siguientes opciones:

1. Integre la autenticación Primetime para agregar comprobaciones de asignación de derechos adicionales antes de la reproducción.
1. Cree un servicio de asignación de derechos local que Primetime Cloud DRM consulta antes de permitir que cualquier dispositivo reproduzca contenido que haya empaquetado.

El servicio local de asignación de derechos debe proporcionar una respuesta a Primetime Cloud DRM que incluya los dos datos siguientes:

* `isAllowed`
* `drmPolicyToUse`

Esto determina si un dispositivo puede reproducir el contenido y qué directiva de DRM se utilizará para generar la licencia de DRM (si `isAllowed` es verdadera).

Este documento cubre lo que debe hacer para lograr la Opción 2 anterior: Implemente su propio servicio de asignación de derechos externo local y póngalo a disposición de Primetime Cloud DRM para el contenido que ha empaquetado.
