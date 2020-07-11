---
description: Una lista de permitidos es una lista de entidades de confianza.
seo-description: Una lista de permitidos es una lista de entidades de confianza.
seo-title: Mantener una lista de permitidos de empaquetadores de contenido de confianza
title: Mantener una lista de permitidos de empaquetadores de contenido de confianza
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Mantener una lista de permitidos de empaquetadores de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Una lista de permitidos es una lista de entidades de confianza.

Para los empaquetadores de contenido, las entidades son organizaciones en las que el propietario del contenido confía para empaquetar (o cifrar) los archivos de vídeo y crear contenido protegido con DRM. Al implementar Adobe Primetime DRM, debe mantener una lista de permitidos de empaquetadores de contenido de confianza. También debe comprobar la identidad del empaquetador de contenido en los metadatos DRM de un archivo protegido con DRM antes de emitir una licencia.

Para obtener información sobre la entidad que empaquetó el contenido, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
