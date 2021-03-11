---
description: Para evitar que los usuarios hagan copias de seguridad y restauren archivos para evitar el desregistro de dominios, debe implementar algunos enfoques de administración de dominios.
title: Administración de dominios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Administración de dominios {#managing-domains}

Para evitar que los usuarios hagan copias de seguridad y restauren archivos para evitar el desregistro de dominios, debe implementar algunos enfoques de administración de dominios.

Estos son algunos enfoques de administración de dominios:

* Limite la cantidad de tiempo que las credenciales del dominio son válidas.

   Los clientes deben ponerse en contacto con el servidor de dominio para volver a adquirir las credenciales de dominio cuando caduquen las credenciales. En ese momento, Domain Server puede verificar que el equipo esté autorizado para ser miembro del dominio.
* Desplácese por las claves de dominio cada vez que un usuario cancele la inscripción.

   El servidor de licencias solo debe emitir licencias a clientes que tengan la última clave de dominio. Este enfoque supone que el servidor de licencias puede coordinarse con el servidor de dominios para saber cuál de las claves es la más reciente. Al pasar el ratón por encima de las claves de dominio, se generará un nuevo par de claves para el dominio. Al pasar el ratón por encima de las claves de un dominio, aumente la versión de clave en `generateDomainCredential`.
* Si el servidor de dominio es el mismo que el servidor de licencias, el servidor puede utilizar el contador de reversión para detectar una copia de seguridad y una restauración.

   Para obtener más información, consulte [Procesamiento de solicitudes DRM de Adobe Primetime](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

