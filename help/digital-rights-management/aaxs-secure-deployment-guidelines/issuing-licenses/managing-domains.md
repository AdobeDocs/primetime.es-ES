---
seo-title: Administración de dominios
title: Administración de dominios
uuid: aee02196-8704-46ee-add9-82b371722f0f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Administración de dominios{#managing-domains}

Para evitar que los usuarios puedan realizar copias de seguridad y restaurar sus archivos con el fin de evitar el desregistro de dominios, se recomienda implementar uno de los siguientes enfoques para la administración de dominios:

* Limite la cantidad de tiempo que las credenciales de dominio son válidas. Los clientes deberán ponerse en contacto con el servidor de dominio para volver a adquirir las credenciales de dominio cuando caduquen. En ese momento, el servidor de dominio puede asegurarse de que el equipo aún está autorizado para ser miembro del dominio.
* Cambie las claves de dominio cada vez que un usuario se desregistra. El servidor de licencias solo debe emitir licencias a clientes que tengan la clave de dominio más reciente. Esto supone que el servidor de licencias puede coordinarse con el servidor de dominios para saber qué clave es la más reciente. Al pasar el ratón por encima de las claves de dominio, se genera un nuevo par de claves para el dominio. Al pasar el ratón por encima de las claves de un dominio concreto, asegúrese de incrementar la versión clave en `generateDomainCredential`. Para obtener más información sobre la implementación de un rollover de clave, consulte *RefImplDomainReqHandler* en Implementación de referencia.
* Si el servidor de dominio es el mismo que el servidor de licencias, el servidor puede utilizar el contador de reversión para detectar la copia de seguridad y la restauración. Consulte *Procesamiento de solicitudes de acceso a Adobe *en *Uso del SDK de acceso a Adobe para la protección de contenido.*

