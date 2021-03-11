---
title: Administración de dominios
description: Administración de dominios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Administración de dominios{#managing-domains}

Para evitar que los usuarios puedan hacer una copia de seguridad y restaurar sus archivos en un esfuerzo por evitar la anulación del registro de dominios, se recomienda implementar uno de los siguientes enfoques para la administración de dominios:

* Limite la cantidad de tiempo que las credenciales del dominio son válidas. Los clientes deberán ponerse en contacto con el servidor de dominio para volver a adquirir las credenciales de dominio cuando caduquen. En ese momento, Domain Server puede garantizar que el equipo esté autorizado para ser miembro del dominio.
* Cambie las claves de dominio cada vez que un usuario cancele el registro. El servidor de licencias solo debe emitir licencias a clientes que tengan la última clave de dominio. Esto supone que el servidor de licencias puede coordinarse con el servidor de dominio para saber cuál es la clave más reciente. Al pasar el ratón por encima de las claves de dominio, se generará un nuevo par de claves para el dominio. Al pasar el ratón por encima de las claves de un dominio determinado, asegúrese de incrementar la versión de clave en `generateDomainCredential`. Para obtener más información sobre la implementación de una sustitución de claves, consulte *RefImplDomainReqHandler* en Implementación de referencia.
* Si el servidor de dominio es el mismo que el servidor de licencias, el servidor puede utilizar el contador de reversión para detectar la copia de seguridad y la restauración. Consulte *Procesamiento de solicitudes de acceso al Adobe *en *Uso del SDK de acceso al Adobe para la protección de contenido.*

