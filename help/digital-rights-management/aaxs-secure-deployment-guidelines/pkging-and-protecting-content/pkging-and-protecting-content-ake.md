---
seo-title: Cifrado de claves asimétricas
title: Cifrado de claves asimétricas
uuid: 0aae25f1-a609-4c73-9aef-13f8ae63f6e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Cifrado de claves asimétricas{#asymmetric-key-encryption}

El cifrado asimétrico de claves (también llamado cifrado de clave pública) utiliza pares de claves. Se utiliza una clave para el cifrado; el otro para descifrado. La clave de descifrado se mantiene en secreto y se denomina clave ** privada. La clave de cifrado, conocida como clave ** pública, está disponible para cualquier persona autorizada para cifrar contenido. Cualquier persona que tenga acceso a la clave pública puede cifrar el contenido, pero sólo alguien con acceso a la clave privada puede descifrarlo. La clave privada no se puede reconstruir a partir de la clave pública.

Al empaquetar contenido, la clave pública del servidor de licencias se utiliza para cifrar la clave de codificación de contenido (CEK) en los metadatos DRM. Debe asegurarse de que sólo el servidor de licencias tiene acceso a la clave privada del servidor de licencias; si otra persona tiene la clave, puede descifrar y ver el contenido.

***Precaución:**Asegúrese de obtener el certificado del servidor de licencias (que contiene la clave pública) de un origen de confianza para asegurarse de que es la clave del servidor de licencias y no una clave pública no fiable. Si un atacante sustituyera su clave pública por la clave del servidor de licencias, podría descifrar su contenido.*

Para obtener más información sobre el empaquetado de contenido, consulte *Uso del SDK de Adobe Access para la protección de contenido*.
