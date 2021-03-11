---
description: Para aquellos familiarizados con la solución Primetime Access DRM de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y el DRM de Primetime Cloud, con tecnología de la solución ExpressPlay.
title: Migración de Access a Multi-DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Migración de Access a Multi-DRM {#migrating-from-access-to-multi-drm}

Para aquellos familiarizados con la solución Primetime Access DRM de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y el DRM de Primetime Cloud, con tecnología de la solución ExpressPlay.

## Diferencias arquitectónicas entre Access y Multi-DRM

|  | Acceso | Multi-DRM |
|---|---|---|
| **Envase** | Packager está enlazado a un servidor de licencias. Packager debe conocer la clave pública del servidor de licencias cuando se empaqueta el contenido. | Packager no está enlazado a un servidor de licencias. |
|  | Una vez empaquetado el contenido, está enlazado a un servidor de licencias en particular. | El contenido no está enlazado a un servidor de licencias específico. Un efecto de esto es que puede empaquetar todo su contenido antes de obtener su licencia de producción. |
|  | El Packager no necesita comunicarse con ninguna forma de almacenamiento de claves, ya que las claves están incrustadas de forma segura en el propio contenido (en los metadatos) después de cifrarse. Solo el servidor de licencias correspondiente puede leerlos. | Las claves deben enviarse *a* Packagers desde un sistema de almacenamiento clave o enviarse *desde* un Packager a un sistema de almacenamiento clave. Un sistema de almacenamiento clave puede ser el propio sistema del cliente o puede ser el Almacenamiento de claves de ExpressPlay. |
| **Derecho** | El cliente realiza una solicitud de contenido al servicio de Access Cloud. A continuación, el servicio en la nube de Access realiza una solicitud al sistema de autorizaciones del cliente. El sistema de autorizaciones del cliente responde con autorizaciones para el cliente. (Es probable que el cliente haya obtenido una cookie para el inicio de sesión de los servidores del cliente antes de realizar la solicitud de licencia). | El cliente realiza una solicitud de un token desde la tienda del cliente (este es probablemente el mismo flujo de trabajo en el que el cliente obtenía previamente una cookie de autenticación). En este momento, el cliente realiza una comprobación de autorizaciones. Si se supera la comprobación de autorizaciones, el cliente envía una solicitud a los servidores de ExpressPlay para generar un token para el cliente. Este token siempre está enlazado a un contenido específico y *puede* estar enlazado a un dispositivo específico. La tienda del cliente envía el token de vuelta al cliente. Cuando el cliente realiza una solicitud de reproducción de DRM, el token se incluye en la solicitud (el método para esto es específico del dispositivo) y el servidor DRM de ExpressPlay valida el token sin llamar al servidor del cliente. |