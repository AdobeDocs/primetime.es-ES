---
seo-title: Primetime DRM en el cliente
title: Primetime DRM en el cliente
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Primetime DRM en el cliente{#primetime-drm-on-the-client}

Una aplicación Primetime TVSDK que reproduce contenido protegido debe llamar primero a las API de DRM de Primetime para iniciar el flujo de trabajo para el consumo de licencias y la reproducción de contenido protegido. En este flujo de trabajo, Primetime DRM en el cliente construye una solicitud de licencia a partir de los metadatos del contenido protegido y, a continuación, la envía al servidor de licencias DRM de Primetime.

Antes de emitir la solicitud de licencia, el cliente puede opcionalmente realizar la autenticación/autorización necesaria (según sus reglas comerciales).
