---
title: Administración de dominios
description: Administración de dominios
copied-description: true
exl-id: c9030373-fd54-4745-9f03-0218532b9d6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Administración de dominios{#managing-domains}

Para evitar que los usuarios puedan realizar copias de seguridad y restaurar sus archivos en un esfuerzo por evitar la anulación del registro del dominio, se recomienda implementar uno de los siguientes métodos para la administración de dominios:

* Limite la cantidad de tiempo que las credenciales de dominio son válidas. Los clientes deberán ponerse en contacto con el servidor de dominio para volver a adquirir las credenciales de dominio cuando caduquen. En ese momento, el servidor de dominio puede asegurarse de que el equipo sigue estando autorizado para ser miembro del dominio.
* Pase el ratón sobre las claves de dominio cada vez que un usuario anule su registro. El servidor de licencias sólo debe emitir licencias a los clientes que tengan la clave de dominio más reciente. Esto supone que el servidor de licencias puede coordinarse con el servidor de dominio para saber qué clave es la más reciente. Para pasar las claves de dominio, se genera un nuevo par de claves para el dominio. Cuando pase el ratón sobre las claves de un dominio concreto, asegúrese de incrementar la versión de la clave en `generateDomainCredential`. Para obtener más información sobre la implementación de una sustitución de claves, consulte *RefImplDomainReqHandler* en la Implementación de referencia.
* Si el servidor de dominio es el mismo que el servidor de licencias, el servidor puede utilizar el contador de reversión para detectar la copia de seguridad y la restauración. Consulte *Procesamiento de solicitudes de acceso al Adobe *en *Uso del SDK de acceso a Adobe para proteger el contenido.*
