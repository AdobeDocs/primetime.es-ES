---
description: Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones de DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Acceso desde el Adobe a Primetime.
title: Información general sobre Multi-DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Flujos de trabajo de varias DRM {#multi-drm-workflows}

Puede implementar varias soluciones DRM para sus aplicaciones TVSDK mediante Primetime DRM Cloud, con tecnología ExpressPlay. Las soluciones de DRM incluyen FairPlay de Apple, Widevine de Google, PlayReady de Microsoft y Acceso desde el Adobe a Primetime.

## Información general sobre Multi-DRM {#multi-drm-overview}

Adobe TVSDK admite la protección DRM mediante varios esquemas DRM. ofertas de Adobe *Primetime DRM Cloud, con tecnología ExpressPlay* para proporcionar el empaquetado, las licencias y la reproducción del contenido de vídeo en varias plataformas.

Los esquemas DRM admitidos incluyen los de Adobe *Acceso a Primetime* DRM (AAXS), así como DRM nativos en varios dispositivos, incluidos [Widevine](https://www.widevine.com) en Chrome y Android, [FairPlay](https://developer.apple.com/streaming/fps/) en Safari y iOS, y [PlayReady](https://www.microsoft.com/playready/) en Edge y XboxOne. Consulte con un representante del Adobe la información sobre los esquemas DRM disponibles actualmente en estas plataformas, así como las fechas programadas de futuras versiones.

TVSDK admite licencias DRM emitidas por cualquier servidor de licencias que utilice estos protocolos. Además de admitir varias soluciones DRM, Adobe ofrece *Primetime DRM Cloud, con tecnología ExpressPlay* como una solución en la que ExpressPlay opera los servidores de licencias para cada solución. Esto puede simplificar la configuración y el mantenimiento para sus necesidades de emisión de licencias DRM.

Para usar *Primetime DRM Cloud, con tecnología ExpressPlay* para implementar sus necesidades de DRM en aplicaciones de TVSDK, primero debe obtener un [ExpressPlay.com](https://www.expressplay.com) cuenta. ExpressPlay proporciona la capacidad de licencia para varios esquemas de protección de DRM diferentes, y también proporciona otros servicios, incluyendo el empaquetado y la administración de claves.

Tu representante de Adobe configurará inicialmente tu cuenta de ExpressPlay. A continuación, puede configurar su cuenta de y obtener la *autenticadores de cliente* que utilizará en las solicitudes de token de licencia a los servidores de ExpressPlay.
