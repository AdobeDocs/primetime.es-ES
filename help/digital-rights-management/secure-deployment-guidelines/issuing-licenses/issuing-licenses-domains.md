---
description: Para evitar que los usuarios realicen copias de seguridad y restauren archivos para evitar la anulación del registro del dominio, debe implementar algunos enfoques de administración de dominios.
title: Administración de dominios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Administración de dominios {#managing-domains}

Para evitar que los usuarios realicen copias de seguridad y restauren archivos para evitar la anulación del registro del dominio, debe implementar algunos enfoques de administración de dominios.

Estos son algunos enfoques de administración de dominios:

* Limite la cantidad de tiempo que las credenciales de dominio son válidas.

  Los clientes deben ponerse en contacto con el servidor de dominio para volver a adquirir las credenciales del dominio cuando caduquen. En ese momento, el servidor de dominio puede comprobar que el equipo aún está autorizado para ser miembro del dominio.
* Pase el ratón sobre las claves de dominio cada vez que un usuario se dé de baja.

  El servidor de licencias sólo debe emitir licencias a los clientes que tengan la clave de dominio más reciente. Este enfoque supone que el servidor de licencias puede coordinarse con el servidor de dominio para saber qué clave es la más reciente. Para pasar las claves de dominio, se genera un nuevo par de claves para el dominio. Cuando transfiera las claves de un dominio, incremente la versión de la clave en `generateDomainCredential`.
* Si el servidor de dominio es el mismo que el servidor de licencias, el servidor puede utilizar el contador de reversión para detectar una copia de seguridad y una restauración.

  Para obtener más información, consulte [Procesamiento de solicitudes de DRM de Adobe Primetime](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
