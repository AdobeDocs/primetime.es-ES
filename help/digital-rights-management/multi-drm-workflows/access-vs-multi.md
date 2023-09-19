---
description: Para aquellos familiarizados con la solución DRM de acceso de Primetime de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y la DRM de nube de Primetime, con tecnología de la solución ExpressPlay.
title: Migración del acceso a Multi-DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Migración del acceso a Multi-DRM {#migrating-from-access-to-multi-drm}

Para aquellos familiarizados con la solución DRM de acceso de Primetime de Adobe, existen algunas diferencias arquitectónicas fundamentales entre Access y la DRM de nube de Primetime, con tecnología de la solución ExpressPlay.

## Diferencias arquitectónicas entre acceso y Multi-DRM

|  | Acceso | Multi-DRM |
|---|---|---|
| **Empaquetando** | El empaquetador está enlazado a un servidor de licencias. El empaquetador debe conocer la clave pública del servidor de licencias cuando se empaqueta el contenido. | El empaquetador no está enlazado a un servidor de licencias. |
|  | Una vez empaquetado el contenido, se enlaza a un servidor de licencias concreto. | El contenido no está enlazado a un servidor de licencias específico. Un efecto de esto es que puede empaquetar todo el contenido antes de obtener la licencia de producción. |
|  | El empaquetador no necesita comunicarse con ningún tipo de almacenamiento de claves, ya que las claves están incrustadas de forma segura en el propio contenido (en metadatos) después de cifrarse. Solo el servidor de licencias correspondiente puede leerlas. | Las claves deben enviarse *hasta* Paquetes de un sistema de almacenamiento de claves o enviados *de* un Packager a un sistema de almacenamiento de claves. Un sistema de almacenamiento de claves puede ser el propio sistema del cliente o puede ser el almacenamiento de claves de ExpressPlay. |
| **Derecho** | El cliente realiza una solicitud de contenido al servicio en la nube de Access. A continuación, el servicio en la nube de Access realiza una solicitud al sistema de asignación de derechos del cliente. El sistema de derechos del cliente responde con derechos para el cliente. (Es probable que el cliente haya recibido una cookie para iniciar sesión desde los servidores del cliente antes de realizar la solicitud de licencia). | El cliente realiza una solicitud de un token desde la tienda del cliente (probablemente sea el mismo flujo de trabajo en el que el cliente recibía anteriormente una cookie de autenticación). En este momento, el cliente realiza una comprobación de derechos. Si se supera la comprobación de derechos, el cliente envía una solicitud a los servidores de ExpressPlay para generar un token para el cliente. Este token siempre está enlazado a un fragmento de contenido específico y *mayo* estar enlazado a un dispositivo específico. La tienda del cliente devuelve el token al cliente. Cuando el cliente realiza una solicitud de reproducción DRM, el token se incluye en la solicitud (el método para esto es específico del dispositivo) y el servidor DRM de ExpressPlay valida el token sin llamar al servidor del cliente. |
