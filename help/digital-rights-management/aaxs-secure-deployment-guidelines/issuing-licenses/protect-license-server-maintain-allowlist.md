---
seo-title: Mantener una lista de permitidos de empaquetadores de contenido de confianza
title: Mantener una lista de permitidos de empaquetadores de contenido de confianza
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Mantener una lista de permitidos de empaquetadores de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Una **lista de permitidos** es una lista de entidades de confianza. En el caso de los empaquetadores de contenido, se trata de organizaciones en las que el propietario del contenido confía para empaquetar (o cifrar) los archivos de vídeo FLV/F4V y crear contenido protegido por DRM. Al implementar Adobe Access, se recomienda mantener una lista de permitidos de empaquetadores de contenido de confianza y comprobar la identidad del empaquetador de contenido contenido contenido en los metadatos DRM (el encabezado DRM) de un archivo protegido por DRM antes de emitir una licencia.

Para obtener más información sobre la obtención de información sobre la entidad que empaquetó el contenido, consulte `V2ContentMetaData.getPackagerInfo()` en la *Referencia de API de acceso a Adobe*.
