---
title: Flujo de trabajo DRM de AXS estándar
description: Flujo de trabajo DRM de AXS estándar
exl-id: 3bc6aa6a-cda6-4c83-af08-f27eb103a47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Flujo de trabajo DRM de AXS estándar{#standard-aaxs-drm-workflow}

1. (Paquete) El SDK de Java de AXS genera una CEK aleatoria.
1. (Paquete) El CEK se utiliza para cifrar contenido.
1. (Paquete) El CEK se cifra utilizando la clave pública del servidor de licencias de AXS.
1. (Paquete) El CEK cifrado se inserta en los metadatos DRM del contenido.
1. El dispositivo intenta reproducir contenido solicitando una licencia al servidor AXS.
1. (Licencias) El servidor AXS utiliza su clave privada para descifrar el CEK de los metadatos.
1. (Licencias) El servidor AXS emite al dispositivo una licencia que contiene el CEK.
