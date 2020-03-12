---
description: Para aquellos familiarizados con la solución DRM de Primetime Access de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y el DRM de Primetime Cloud, con la tecnología de la solución ExpressPlay.
seo-description: Para aquellos familiarizados con la solución DRM de Primetime Access de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y el DRM de Primetime Cloud, con la tecnología de la solución ExpressPlay.
seo-title: Migración de Access a Multi-DRM
title: Migración de Access a Multi-DRM
uuid: 3e33ca9a-867e-46b8-bf88-8dbfe14ff786
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Migración de Access a Multi-DRM {#migrating-from-access-to-multi-drm}

Para aquellos familiarizados con la solución DRM de Primetime Access de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y el DRM de Primetime Cloud, con la tecnología de la solución ExpressPlay.

## Diferencias arquitectónicas entre el acceso y los múltiples DRM

|  | Acceso | Multi-DRM |
|---|---|---|
| **Empaquetado** | Packager está enlazado a un servidor de licencias. Packager debe conocer la clave pública del servidor de licencias cuando se empaqueta el contenido. | Packager no está enlazado a un servidor de licencias. |
|  | Una vez empaquetado el contenido, se vincula a un servidor de licencias concreto. | El contenido no está enlazado a un servidor de licencias específico. Un efecto de esto es que puede empaquetar todo su contenido antes de obtener su licencia de producción. |
|  | Packager no necesita comunicarse con ninguna forma de almacenamiento de claves, ya que las claves se incrustan de forma segura en el propio contenido (en metadatos) después de cifrarse. Sólo el servidor de licencias correspondiente puede leerlos. | Las claves se deben enviar *a los* Packagers desde un sistema de almacenamiento clave o *desde* Packager a un sistema de almacenamiento clave. Un sistema de almacenamiento clave puede ser el propio sistema del cliente o puede ser el Almacenamiento de claves de ExpressPlay. |
| **Asignación de derechos** | El cliente realiza una solicitud de contenido al servicio de Access Cloud. A continuación, el servicio en la nube de Access realiza una solicitud al sistema de asignación de derechos del cliente. El sistema de asignación de derechos del cliente responde con los derechos del cliente. (Es probable que el cliente haya obtenido una cookie de inicio de sesión de los servidores del cliente antes de realizar la solicitud de licencia). | El cliente realiza una solicitud de un token desde la tienda del cliente (este es probablemente el mismo flujo de trabajo en el que el cliente recibía previamente una cookie de autenticación). En este momento, el cliente realiza una comprobación de derechos. Si se aprueba la comprobación de derechos, el cliente envía una solicitud a los servidores ExpressPlay para generar un token para el cliente. Este token siempre está enlazado a un contenido específico y *puede* estar enlazado a un dispositivo específico. La tienda del cliente devuelve el token al cliente. Cuando el cliente realiza una solicitud de reproducción de DRM, el token se incluye en la solicitud (el método para esto es específico del dispositivo) y el servidor DRM de ExpressPlay valida el token sin llamar al servidor del cliente. |