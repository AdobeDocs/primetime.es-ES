---
title: Cifrado de claves asimétricas
description: Cifrado de claves asimétricas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Cifrado de claves asimétricas{#asymmetric-key-encryption}

El cifrado de claves asimétricas (también denominado cifrado de claves públicas) utiliza pares de claves. Se utiliza una clave para el cifrado; el otro para el descifrado. La clave de descifrado se mantiene en secreto y se denomina *clave privada*. La clave de cifrado, denominada *clave pública*, está disponible para cualquier persona autorizada para cifrar contenido. Cualquier persona con acceso a la clave pública puede cifrar el contenido, pero solo alguien con acceso a la clave privada puede descifrarlo. La clave privada no se puede reconstruir a partir de la clave pública.

Al empaquetar contenido, la clave pública del servidor de licencias se utiliza para cifrar la clave de cifrado de contenido (CEK) en los metadatos de DRM. Debe asegurarse de que solo el servidor de licencias tenga acceso a la clave privada del servidor de licencias; si otra persona tiene la clave, puede descifrar y ver el contenido.

***Precaución:**asegúrese de obtener el certificado del servidor de licencias (que contiene la clave pública) de una fuente de confianza, de modo que pueda estar seguro de que es la clave del servidor de licencias y no una clave pública no fiable. Si un atacante reemplazara su clave pública por la clave del servidor de licencias, podría descifrar su contenido.*

Para obtener más información sobre el contenido del paquete, consulte *Uso del SDK de acceso a Adobe para la protección de contenido*.
