---
title: Mantener una lista de permitidos de paquetes de contenido de confianza
description: Mantener una lista de permitidos de paquetes de contenido de confianza
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Mantener una lista de permitidos de paquetes de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Un **lista de permitidos** es una lista de entidades de confianza. En el caso de los empaquetadores de contenido, se trata de organizaciones en las que el propietario del contenido confía para empaquetar (o cifrar) los archivos de vídeo FLV/F4V y crear contenido protegido por DRM. Al implementar el acceso de Adobe, se recomienda mantener una lista de permitidos de empaquetadores de contenido de confianza y comprobar la identidad del empaquetador de contenido incluido en los metadatos DRM (el encabezado DRM) de un archivo protegido por DRM antes de emitir una licencia.

Para obtener más información sobre la obtención de información acerca de la entidad que empaquetó el contenido, consulte `V2ContentMetaData.getPackagerInfo()` en el *Referencia de API de acceso de Adobe*.
