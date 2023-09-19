---
title: Cifrado de clave asimétrica
description: Cifrado de clave asimétrica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Cifrado de clave asimétrica{#asymmetric-key-encryption}

El cifrado de clave asimétrica (también denominado cifrado de clave pública) utiliza pares de claves. Una clave se utiliza para el cifrado y la otra para el descifrado. La clave de descifrado se mantiene en secreto y se denomina *clave privada*. La clave de cifrado, denominada *clave pública*, se pone a disposición de cualquier persona autorizada para cifrar contenido. Cualquier persona con acceso a la clave pública puede cifrar el contenido, pero solamente alguien con acceso a la clave privada puede descifrarlo. La clave privada no se puede reconstruir a partir de la clave pública.

Al empaquetar contenido, se utiliza la clave pública del servidor de licencias para cifrar la clave de cifrado de contenido (CEK) en los metadatos DRM. Debe asegurarse de que solo el servidor de licencias tiene acceso a la clave privada del servidor de licencias; si otra persona tiene la clave, puede descifrar y ver el contenido.

***Precaución:**Asegúrese de obtener el certificado del servidor de licencias (que contiene la clave pública) de una fuente de confianza para poder estar seguro de que es la clave del servidor de licencias y no una clave pública no fiable. Si un atacante sustituyera la clave pública por la del servidor de licencias, podría descifrar el contenido.*

Para obtener más información sobre el contenido de los paquetes, consulte *Uso del SDK de acceso a Adobe para proteger el contenido*.
