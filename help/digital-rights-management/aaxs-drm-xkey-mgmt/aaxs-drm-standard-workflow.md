---
title: Flujo de trabajo DRM AAXS estándar
description: Flujo de trabajo DRM AAXS estándar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Flujo de trabajo DRM AAXS estándar{#standard-aaxs-drm-workflow}

1. (Paquete) El SDK de Java AAXS genera un CEK aleatorio.
1. (Paquete) El CEK se utiliza para cifrar contenido.
1. (Paquete) El CEK se cifra utilizando la clave pública del servidor de licencias AAXS.
1. (Paquete) El CEK cifrado se inserta en los metadatos DRM del contenido.
1. El dispositivo intenta reproducir contenido solicitando una licencia del servidor AAXS.
1. (Licencias) El servidor AAXS utiliza su clave privada para descifrar el CEK de los metadatos.
1. (Licencias) El servidor AAXS emite al dispositivo una licencia que contiene el CEK.
