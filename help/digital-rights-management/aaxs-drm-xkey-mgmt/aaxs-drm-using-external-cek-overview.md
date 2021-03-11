---
description: Los clientes pueden utilizar el DRM de acceso al Adobe (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externo.
title: Información general del CEK externo de DRM de acceso al Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Información general del CEK externo de DRM de acceso al Adobe {#adobe-access-drm-external-cek-overview}

Los clientes pueden utilizar el DRM de acceso al Adobe (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externo.

DRM de acceso a Adobe (AAXS), de forma predeterminada, abstrae la necesidad de gestionar directamente claves, certificados y metadatos DRM durante el proceso de empaquetado de contenido. El SDK de Java AAXS genera automáticamente una clave de cifrado de contenido (CEK) aleatoria durante el empaquetado y la utiliza para cifrar el contenido. A continuación, el SDK cifra el propio CEK y lo inserta en los metadatos del contenido. En el momento de la emisión de la licencia, el servidor AAXS solo necesita su clave privada del servidor de licencias AAXS para acceder al CEK desde los metadatos para generar una licencia.
