---
title: Mantener una lista de permitidos de paquetes de contenido de confianza
description: Mantener una lista de permitidos de paquetes de contenido de confianza
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Mantener una lista de permitidos de paquetes de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Una **lista de permitidos** es una lista de entidades de confianza. En el caso de los paquetes de contenido, estas son organizaciones en las que el propietario del contenido confía para empaquetar (o encriptar) los archivos de vídeo FLV/F4V, creando contenido protegido por DRM. Al implementar Adobe Access, se recomienda mantener una lista de permitidos de paquetes de contenido de confianza y comprobar la identidad del paquete de contenido contenido contenido en los metadatos DRM (el encabezado DRM) de un archivo protegido DRM antes de emitir una licencia.

Para obtener más información sobre la obtención de información sobre la entidad que empaquetó el contenido, consulte `V2ContentMetaData.getPackagerInfo()` en la *Referencia de API de acceso al Adobe*.
