---
description: En ocasiones, habrá ocasiones en que el contenido no se pueda reproducir. Cualquier número de situaciones puede causar esto, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución del Flash Player o el sistema DRM de Primetime.
title: Resumen de errores de prueba
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Activación de errores {#triaging-errors}

En ocasiones, habrá ocasiones en que el contenido no se pueda reproducir. Cualquier número de situaciones puede causar esto, incluidos errores en la pila de red del explorador, la capa de transporte, el sistema operativo, el tiempo de ejecución del Flash Player o el sistema DRM de Primetime.

El primer paso de diagnóstico es determinar si el problema se manifiesta sin el cifrado DRM introducido en la ecuación. Intente empaquetar el contenido, pero indique al empaquetador que no lo cifre. Si el problema persiste, es probable que se trate de un problema de codificación o empaquetado del contenido, o en algún lugar de la infraestructura de red. Si el problema desaparece cuando el contenido se empaqueta sin cifrado, es probable que el error de reproducción se deba a un problema de DRM y debería realizar una prueba cliente/servidor.

Primetime DRM (fuera de Primetime Cloud DRM) ha estado en el mercado durante varios años. Como tal, existe una gran cantidad de información de origen comunitario sobre la resolución de problemas y la configuración de DRM de Primetime. Adobe ha proporcionado un foro para que los usuarios de Primetime DRM (anteriormente denominado Acceso al Adobe) sumen y compartan problemas y resoluciones. Para determinar si su problema se ha tratado anteriormente, compruebe: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Activación de errores de cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Si el contenido no se reproduce, examine el panel derecho de los reproductores de vídeo de muestra, que registrarán cualquier `DRMErrorEvent` que ocurre. Si hay un evento de error, se correlacionará con uno de los errores de tiempo de ejecución de Flash Player:

* [Referencia de mensaje de error del cliente DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages); o
* [Errores de tiempo de ejecución de Flash AS3](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (Los problemas de DRM comienzan a las 3300)
