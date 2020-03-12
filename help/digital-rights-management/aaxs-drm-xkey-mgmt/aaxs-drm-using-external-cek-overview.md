---
description: Los clientes pueden utilizar DRM de Adobe Access (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externo.
seo-description: Los clientes pueden utilizar DRM de Adobe Access (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externo.
seo-title: Información general de CEK externo de DRM de Adobe Access
title: Información general de CEK externo de DRM de Adobe Access
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97

---


# Información general de CEK externo de DRM de Adobe Access {#adobe-access-drm-external-cek-overview}

Los clientes pueden utilizar DRM de Adobe Access (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externo.

De forma predeterminada, Adobe Access (AAXS) DRM abstrae la necesidad de gestionar directamente claves, certificados y metadatos DRM durante el proceso de empaquetado de contenido. El SDK de Java AAXS generará automáticamente una clave de cifrado de contenido (CEK) aleatoria durante el tiempo de empaquetado y la usará para cifrar el contenido. A continuación, el SDK codifica el propio CEK y lo inserta en los metadatos del contenido. En el momento de la emisión de la licencia, el servidor AAXS solo necesita su clave privada de servidor de licencias AAXS para acceder al CEK desde los metadatos y generar una licencia.
