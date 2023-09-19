---
title: Implementación de certificados
description: Implementación de certificados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Implementación de certificados{#deploy-certificates}

Para evitar que la contraseña PFX esté disponible en texto no cifrado en el servidor de licencias, la Implementación de referencia y el Servidor DRM de Adobe Primetime para transmisión protegida requieren que la contraseña se cifre cuando se especifica en el archivo de configuración. Consulte *Uso de las implementaciones de referencia de DRM de Primetime* o *Uso del servidor DRM de Primetime* para Flujo protegido, para obtener instrucciones sobre cómo ejecutar las utilidades de codificado. Cada uno de ellos incluye su propia utilidad de descifrado, y las contraseñas cifradas no son intercambiables entre estas dos implementaciones del servidor de licencias.

Para implementar los certificados y las contraseñas codificadas en el servidor de licencias, consulte *Uso de las implementaciones de referencia de DRM de Primetime* o *Uso del servidor DRM de Primetime para flujo protegido*.
