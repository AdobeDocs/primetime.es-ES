---
title: Notas de la versión de Primetime
description: Notas de la versión de Primetime
copied-description: true
exl-id: 29087a3e-f16e-4510-8d3a-ed2229700899
source-git-commit: fe0f5f3399d2e2ab3e07713fbcd29ede47888d98
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 31%

---

# Notas de la versión de Primetime

Le damos la bienvenida a las notas de la versión de Adobe Primetime. Los documentos enumerados en la navegación de la izquierda proporcionan información específica sobre la versión, requisitos del sistema, limitaciones, problemas corregidos y problemas conocidos.

## Mejoras y correcciones en PTAI 21.5.1

La versión incluye nueva telemetría para los próximos cambios en el tablero, y compatibilidad con el tipo de segmentación obsoleta 0x01 (UPID) para formatos de referencia basados en SCTE.

Para obtener más correcciones y detalles, consulte [Notas de la versión del Ad Insertion](/help/release-notes/ptai-21x-release-notes.md)

## Mejoras y correcciones en TVSDK 3.13 iOS

La versión incorpora compatibilidad con los anuncios DEMUXED &#39;HLS/CMAF&#39; (preroll, midroll y postroll) para emisiones en directo, VOD y FER.

Para obtener más correcciones y detalles, consulte [TVSDK for iOS Release Notes](../release-notes/tvsdk-3x-ios.md)

## Correcciones en TVSDK 3.13 para Android

Esta versión ofrece una solución alternativa al problema de la congelación del flujo Widevine DRM o la visualización de marcos negros en el conmutador ABR en dispositivos FireTV, que incluyen dispositivos de 1ª y 2ª generación del Pendant Fire TV y del Cubo Fire TV de 1ª y 2ª generación.

Para resolver el problema, establezca la API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` para los dispositivos Fire TV especificados antes de iniciar la reproducción. El valor predeterminado es false.

Consulte las [Notas de la versión de TVSDK para Android](../release-notes/tvsdk-3x-android.md) para obtener más información.

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
