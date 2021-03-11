---
description: En ocasiones, habrá momentos en que el contenido no se pueda reproducir. Cualquier cantidad de situaciones pueden causar esto, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución del Flash Player o el sistema DRM de Primetime.
title: Información general sobre errores de prueba
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Prueba de errores {#triaging-errors}

En ocasiones, habrá momentos en que el contenido no se pueda reproducir. Cualquier cantidad de situaciones pueden causar esto, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución del Flash Player o el sistema DRM de Primetime.

El primer paso de diagnóstico es determinar si el problema se manifiesta sin el cifrado DRM introducido en la ecuación. Intente empaquetar el contenido, pero indique al empaquetador que no cifra el contenido. Si el problema persiste, es probable que se trate de un problema de codificación o empaquetado del contenido, o de algún lugar de la infraestructura de red. Si el problema desaparece cuando el contenido se empaqueta sin cifrado, es probable que el fallo de reproducción se deba a un problema de DRM y debe realizar una prueba cliente/servidor.

Primetime DRM (fuera de Primetime Cloud DRM) ha estado en el mercado durante varios años. Como tal, existe una gran cantidad de información de origen comunitario sobre la solución de problemas y la configuración de Primetime DRM. Adobe ha proporcionado un foro para los usuarios de Primetime DRM (antes llamado Acceso a Adobe) para agregar y compartir problemas y resoluciones. Para determinar si su problema se ha discutido anteriormente, consulte: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Prueba de error de cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Si el contenido no se reproduce, examine el panel derecho de los reproductores de vídeo de muestra, que registrarán cualquier `DRMErrorEvent` que se produzca. Si hay un evento de error, se correlacionará con uno de los errores de tiempo de ejecución de Flash Player :

* [Referencia](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages) de mensajes de error de cliente DRM; o
* [Errores de tiempo de ejecución de Flash AS3](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html)  (los problemas de DRM empiezan en 3300)

