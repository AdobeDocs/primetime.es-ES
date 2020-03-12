---
seo-title: Flujo de trabajo de DRM AAXS estándar
title: Flujo de trabajo de DRM AAXS estándar
description: Flujo de trabajo de DRM AAXS estándar
seo-description: Flujo de trabajo de DRM AAXS estándar
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc

---


# Flujo de trabajo de DRM AAXS estándar{#standard-aaxs-drm-workflow}

1. (Paquete) El SDK de Java AAXS genera un CEK aleatorio.
1. (Paquete) El CEK se utiliza para cifrar contenido.
1. (Paquete) El CEK se cifra mediante la clave pública del servidor de licencias AAXS.
1. (Paquete) El CEK cifrado se inserta en los metadatos DRM del contenido.
1. El dispositivo intenta reproducir contenido solicitando una licencia del servidor AAXS.
1. (Licencias) El servidor AAXS utiliza su clave privada para descifrar el CEK de los metadatos.
1. (Licencias) El servidor AAXS emite al dispositivo una licencia que contiene el CEK.
