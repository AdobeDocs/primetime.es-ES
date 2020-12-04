---
description: Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Primetime Access desde Adobe.
seo-description: Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Primetime Access desde Adobe.
seo-title: Descripción general de Multi-DRM
title: Descripción general de Multi-DRM
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# Flujos de trabajo de varios DRM {#multi-drm-workflows}

Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Primetime Access desde Adobe.

## Información general de Multi-DRM {#multi-drm-overview}

Adobe TVSDK admite la protección DRM mediante varios esquemas DRM. Adobe ofertas *Primetime DRM Cloud, con tecnología ExpressPlay* para proporcionar empaquetado, licencia y reproducción del contenido de vídeo en varias plataformas.

Los esquemas de DRM admitidos incluyen el *Acceso a Primetime* DRM (AAXS) del Adobe, así como los DRM nativos en varios dispositivos, incluidos [Widevine](https://www.widevine.com) en Chrome y Android, [FairPlay](https://developer.apple.com/streaming/fps/) en Safari e iOS y [PlayReady](https://www.microsoft.com/playready/) en Chrome y Android XboxOne. Consulte con un representante de Adobe para obtener información sobre los esquemas DRM que están disponibles actualmente en estas plataformas, así como las fechas programadas para futuras versiones.

TVSDK admite licencias DRM emitidas por cualquier servidor de licencias que utilice estos protocolos. Además de la compatibilidad con varias soluciones DRM, Adobe ofertas *Primetime DRM Cloud, con ExpressPlay* como una solución en la que ExpressPlay opera los servidores de licencias para cada solución. Esto puede simplificar la configuración y el mantenimiento de sus necesidades de emisión de licencias de DRM.

Para utilizar *Primetime DRM Cloud, con tecnología ExpressPlay* para implementar sus necesidades de DRM en aplicaciones de TVSDK, primero debe obtener una cuenta [ExpressPlay.com](https://www.expressplay.com). ExpressPlay proporciona la capacidad de licencia para varios esquemas de protección DRM diferentes, y también ofrece otros servicios, incluyendo empaquetado y administración de claves.

El representante de Adobe configurará inicialmente su cuenta de ExpressPlay. A continuación, puede configurar su cuenta y obtener los *autenticadores de cliente* que utilizará en las solicitudes de token de licencia a los servidores ExpressPlay.