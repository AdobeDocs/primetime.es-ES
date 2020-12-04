---
description: En ocasiones, habrá ocasiones en las que el contenido no se puede reproducir. Esto puede deberse a cualquier número de situaciones, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución de Flash Player o el sistema DRM Primetime.
seo-description: En ocasiones, habrá ocasiones en las que el contenido no se puede reproducir. Esto puede deberse a cualquier número de situaciones, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución de Flash Player o el sistema DRM Primetime.
seo-title: Información general sobre los errores de prueba
title: Información general sobre los errores de prueba
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# Errores de prueba {#triaging-errors}

En ocasiones, habrá ocasiones en las que el contenido no se puede reproducir. Esto puede deberse a cualquier número de situaciones, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución de Flash Player o el sistema DRM Primetime.

El primer paso de diagnóstico es determinar si el problema se manifiesta sin la codificación DRM introducida en la ecuación. Intente empaquetar el contenido, pero indique al empaquetador que no lo codifique. Si el problema persiste, es probable que se trate de un problema de codificación o empaquetado del contenido, o de algún lugar de la infraestructura de red. Si el problema desaparece cuando el contenido se empaqueta sin cifrado, es probable que el error de reproducción se deba a un problema de DRM y debe participar en la prueba cliente/servidor.

Primetime DRM (fuera de Primetime Cloud DRM) ha estado en el mercado durante varios años. Como tal, existe una gran cantidad de información de origen comunitario sobre la solución de problemas y la configuración de Primetime DRM. Adobe ha proporcionado un foro para que los usuarios de Primetime DRM (anteriormente llamado Adobe Access) puedan acumulados y compartir problemas y resoluciones. Para determinar si el problema se ha discutido anteriormente, consulte: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Prueba de error del cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Si el contenido no se reproduce, examine el panel derecho de los Reproductores de video de muestra, que registrará cualquier `DRMErrorEvent` que se produzca. Si hay un evento de error, se correlacionará con uno de los errores de tiempo de ejecución de Flash Player:

* [Referencia](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages) de mensajes de error del cliente DRM; o
* [Errores](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html)  en tiempo de ejecución de Flash AS3(DRM emite inicio a 3300)

