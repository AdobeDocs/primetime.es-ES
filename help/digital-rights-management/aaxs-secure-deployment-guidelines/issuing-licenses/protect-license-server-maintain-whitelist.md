---
seo-title: Mantener una lista blanca de empaquetadores de contenido de confianza
title: Mantener una lista blanca de empaquetadores de contenido de confianza
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Mantener una lista blanca de empaquetadores de contenido de confianza{#maintain-a-whitelist-of-trusted-content-packagers}

Una *lista blanca* es una lista de entidades de confianza. En el caso de los empaquetadores de contenido, se trata de organizaciones en las que el propietario del contenido confía para empaquetar (o cifrar) los archivos de vídeo FLV/F4V y crear contenido protegido por DRM. Al implementar Adobe Access, se recomienda mantener una lista blanca de empaquetadores de contenido de confianza y verificar la identidad del empaquetador de contenido incluido en los metadatos DRM (el encabezado DRM) de un archivo protegido por DRM antes de emitir una licencia.

Para obtener más información sobre la obtención de información sobre la entidad que empaquetó el contenido, consulte `V2ContentMetaData.getPackagerInfo()` la Referencia *de API de* Adobe Access.
