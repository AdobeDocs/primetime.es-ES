---
description: Para evitar que los usuarios realicen copias de seguridad y restauren archivos para evitar el desregistro de dominios, debe implementar algunos enfoques de administración de dominios.
seo-description: Para evitar que los usuarios realicen copias de seguridad y restauren archivos para evitar el desregistro de dominios, debe implementar algunos enfoques de administración de dominios.
seo-title: Administración de dominios
title: Administración de dominios
uuid: 30b73e38-d6ed-43c6-89ba-ae8616383779
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Administración de dominios {#managing-domains}

Para evitar que los usuarios realicen copias de seguridad y restauren archivos para evitar el desregistro de dominios, debe implementar algunos enfoques de administración de dominios.

Estos son algunos enfoques de administración de dominios:

* Limite la cantidad de tiempo que las credenciales de dominio son válidas.

   Los clientes deben ponerse en contacto con el servidor de dominio para volver a adquirir las credenciales de dominio cuando caduquen. En ese momento, el servidor de dominio puede comprobar que el equipo aún está autorizado para ser miembro del dominio.
* Desplácese por las claves de dominio cada vez que un usuario cancele el registro.

   El servidor de licencias solo debe emitir licencias a clientes que tengan la clave de dominio más reciente. Este enfoque supone que el servidor de licencias puede coordinarse con el servidor de dominios para saber qué clave es la más reciente. Al pasar el ratón por encima de las claves de dominio, se genera un nuevo par de claves para el dominio. Al pasar el cursor sobre las claves de un dominio, incremente la versión clave en `generateDomainCredential`.
* Si el servidor de dominio es el mismo que el servidor de licencias, el servidor puede utilizar el contador de reversión para detectar una copia de seguridad y una restauración.

   Para obtener más información, consulte [Procesamiento de solicitudes DRM de Adobe Primetime](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

