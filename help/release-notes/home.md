---
title: Notas de la versión de Primetime
description: Notas de la versión de Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 29%

---


# Notas de la versión de Primetime

Le damos la bienvenida a las notas de la versión de Adobe Primetime. Los documentos enumerados en la navegación de la izquierda proporcionan información específica sobre la versión, requisitos del sistema, limitaciones, problemas corregidos y problemas conocidos.

## Mejoras y correcciones en TVSDK 3.13 iOS

La versión incorpora compatibilidad con los anuncios DEMUXED &#39;HLS/CMAF&#39; (preroll, midroll y postroll) para emisiones en directo, VOD y FER.

Para obtener más correcciones y detalles, consulte [TVSDK for iOS Release Notes](../release-notes/tvsdk-3x-ios.md)

## Mejoras y correcciones en PTAI 21.2.2

La versión incluye compatibilidad con la inserción/sincronización de flujo EXT-X-IMAGE-STREAM-INF en flujos HLS. La función se habilita mediante una configuración del lado del servidor. Póngase en contacto con el representante de cuentas técnicas para habilitar la función.

## Correcciones en TVSDK 3.13 para Android

Esta versión ofrece una solución alternativa al problema de la congelación del flujo Widevine DRM o la visualización de marcos negros en el conmutador ABR en dispositivos FireTV, que incluyen dispositivos de 1ª y 2ª generación del Pendant Fire TV y del Cubo Fire TV de 1ª y 2ª generación.

Para resolver el problema, establezca la API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` para los dispositivos Fire TV especificados antes de iniciar la reproducción. El valor predeterminado es false.

Consulte las [Notas de la versión de TVSDK para Android](../release-notes/tvsdk-3x-android.md) para obtener más información.

## Mejoras y correcciones en las notas de la versión de iOS TVSDK 3.12

La versión se centra en resolver los principales problemas de los clientes.

Consulte para obtener más información sobre la versión actual publicada para [iOS](../release-notes/tvsdk-3x-ios.md).

## Consulte también

| Guía del usuario | Descripción |
|--- |--- |
| [Ayuda de programación de Primetime](/help/programming/home.md) | Le permite aprender a desarrollar aplicaciones y reproductores de vídeo mediante Java en dispositivos Android y Objective-C en dispositivos iOS. |
| [Ayuda de conversión y migración de Primetime](/help/migration-guides/home.md) | Explica el proceso de conversión y migración para pasar de su grupo de TVSDK de Primetime existente al grupo de próxima generación. |
| [Implementación de referencia](/help/android-reference-implementation/home.md) | Ayuda a comprender el SDK de TVSDK y a modificar los administradores de funciones para personalizar su reproductor personal. |
| [Referencias de la API de Primetime](/help/reference/api-references.md) | Proporciona información detallada sobre las funciones de TVSDK, las estructuras de datos y otras construcciones de programación. |
| [Digital Rights Management](/help/digital-rights-management/home.md) | Ayuda a conocer mejor los distintos casos de usuario en Digital Rights Management (DRM) |
| [Ayuda de Primetime Ad Insertion](/help/primetime-ad-insertion/home.md) | Explica cómo monetizar el contenido mediante la inserción de publicidad dinámica dirigida por el usuario en el servidor y captar la atención de la audiencia con anuncios personalizados. |
| [Archivos](https://helpx.adobe.com/primetime/archives.html) | Descargue archivos PDF de la documentación archivada. |

## Recursos útiles

* [Conozca Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [Supervisión de la concurrencia](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Autenticación de Primetime](https://tve.helpdocsonline.com/home)

* [Foros DRM de Adobe Primetime](https://forums.adobe.com/community/adobe_access)

* [Recursos para desarrolladores de Adobe Primetime](https://www.adobe.com/devnet/primetime.html)
