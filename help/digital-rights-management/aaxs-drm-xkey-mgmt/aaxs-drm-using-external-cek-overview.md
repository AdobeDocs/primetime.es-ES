---
description: Los clientes pueden utilizar la DRM de acceso al Adobe (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externa.
title: Descripción general de CEK externo de DRM de acceso a Adobe
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Descripción general de CEK externo de DRM de acceso a Adobe {#adobe-access-drm-external-cek-overview}

Los clientes pueden utilizar la DRM de acceso al Adobe (AAXS) con sus propios sistemas de administración de claves de contenido (CKMS) con la función CEK externa.

De forma predeterminada, el DRM de acceso a Adobe (AAXS) abstrae la necesidad de gestionar directamente claves, certificados y metadatos de DRM durante el proceso de empaquetado de contenido. El SDK de Java de AXS generará automáticamente una clave de cifrado de contenido (CEK) aleatoria durante el tiempo de empaquetado y la utilizará para cifrar el contenido. A continuación, el SDK cifra la propia CEK y la inserta en los metadatos del contenido. En el momento de la emisión de la licencia, el servidor AXS solo necesita su clave privada del servidor de licencias AXS para acceder al CEK desde los metadatos para generar una licencia.
