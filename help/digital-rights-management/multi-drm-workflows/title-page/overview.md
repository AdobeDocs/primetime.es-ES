---
description: Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Primetime Access desde el Adobe.
title: Información general de Multi-DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Flujos de trabajo de varios DRM {#multi-drm-workflows}

Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Primetime Access desde el Adobe.

## Información general de Multi-DRM {#multi-drm-overview}

Adobe TVSDK admite la protección DRM mediante varios esquemas DRM. Adobe ofrece *Primetime DRM Cloud, con tecnología ExpressPlay* para proporcionar paquetes, licencias y reproducción del contenido de vídeo en varias plataformas.

Los esquemas de DRM admitidos incluyen el *Acceso de Primetime* DRM (AAXS) del Adobe, así como los DRM nativos en varios dispositivos, incluidos [Widevine](https://www.widevine.com) en Chrome y Android, [FairPlay](https://developer.apple.com/streaming/fps/) en Safari e iOS y [PlayReady](https://www.microsoft.com/playready/) en Edge y XboxOne. Consulte con un representante de Adobes para obtener información sobre los esquemas DRM que están disponibles actualmente en estas plataformas, así como las fechas programadas de futuras versiones.

TVSDK admite licencias DRM emitidas por cualquier servidor de licencias que utilice estos protocolos. Además de la compatibilidad con varias soluciones DRM, Adobe ofrece *Primetime DRM Cloud, con tecnología ExpressPlay* como solución en la que ExpressPlay opera los servidores de licencias para cada solución. Esto puede simplificar la configuración y el mantenimiento de sus necesidades de emisión de licencias DRM.

Para utilizar *Primetime DRM Cloud, con tecnología ExpressPlay* para implementar sus necesidades de DRM en aplicaciones TVSDK, primero debe obtener una cuenta [ExpressPlay.com](https://www.expressplay.com). ExpressPlay proporciona la capacidad de licencia para varios esquemas de protección DRM diferentes, y también proporciona otros servicios, incluyendo empaquetado y administración de claves.

Su representante de Adobe configurará inicialmente su cuenta de ExpressPlay. A continuación, puede configurar su cuenta y obtener los *autenticadores de cliente* que utilizará en las solicitudes de token de licencia a los servidores de ExpressPlay.