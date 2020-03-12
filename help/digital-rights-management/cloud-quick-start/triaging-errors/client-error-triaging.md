---
description: En ocasiones, habrá ocasiones en las que el contenido no se puede reproducir. Esto puede deberse a cualquier número de situaciones, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución de Flash Player o el sistema Primetime DRM.
seo-description: En ocasiones, habrá ocasiones en las que el contenido no se puede reproducir. Esto puede deberse a cualquier número de situaciones, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución de Flash Player o el sistema Primetime DRM.
seo-title: Información general sobre los errores de prueba
title: Información general sobre los errores de prueba
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Errores de prueba {#triaging-errors}

En ocasiones, habrá ocasiones en las que el contenido no se puede reproducir. Esto puede deberse a cualquier número de situaciones, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución de Flash Player o el sistema Primetime DRM.

El primer paso de diagnóstico es determinar si el problema se manifiesta sin la codificación DRM introducida en la ecuación. Intente empaquetar el contenido, pero indique al empaquetador que no lo codifique. Si el problema persiste, es probable que se trate de un problema de codificación o empaquetado del contenido, o de algún lugar de la infraestructura de red. Si el problema desaparece cuando el contenido se empaqueta sin cifrado, es probable que el error de reproducción se deba a un problema de DRM y debe participar en la prueba cliente/servidor.

Primetime DRM (fuera de Primetime Cloud DRM) ha estado en el mercado durante varios años. Como tal, existe una gran cantidad de información de origen comunitario sobre la solución de problemas y la configuración de Primetime DRM. Adobe ha proporcionado un foro para los usuarios de DRM Primetime (anteriormente denominados Adobe Access) para agregar y compartir problemas y resoluciones. Para determinar si el problema se ha discutido anteriormente, consulte: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Prueba de errores del cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Si el contenido no se reproduce, examine el panel derecho de los Reproductores de video de muestra, que registrarán `DRMErrorEvent` los que se produzcan. Si hay un evento de error, se correlacionará con uno de los errores en tiempo de ejecución de Flash Player:

* [Referencia](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)de mensajes de error del cliente DRM; o
* [Errores](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) de AS3 Flash Runtime (los problemas de DRM empiezan en 3300)

