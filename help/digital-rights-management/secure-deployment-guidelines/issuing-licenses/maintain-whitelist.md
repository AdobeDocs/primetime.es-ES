---
description: Una lista de permitidos es una lista de entidades de confianza.
title: Mantener una lista de permitidos de paquetes de contenido de confianza
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Mantener una lista de permitidos de paquetes de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Una lista de permitidos es una lista de entidades de confianza.

En el caso de los empaquetadores de contenido, las entidades son organizaciones en las que el propietario de contenido confía para empaquetar (o cifrar) los archivos de vídeo y crear contenido protegido por DRM. Al implementar Adobe Primetime DRM, debe mantener una lista de permitidos de paquetes de contenido de confianza. También debe verificar la identidad del empaquetador de contenido en los metadatos DRM de un archivo protegido por DRM antes de emitir una licencia.

Para obtener información sobre la entidad que empaquetó el contenido, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
