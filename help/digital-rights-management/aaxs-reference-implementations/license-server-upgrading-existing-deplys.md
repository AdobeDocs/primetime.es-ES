---
title: Actualización de implementaciones existentes
description: Actualización de implementaciones existentes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Actualización de implementaciones existentes {#upgrading-existing-deployments}

Para actualizar un servidor que ejecute el servidor de licencias de implementación de referencia de versión 3.0 o el paquete de carpetas vigiladas, reemplace los archivos [!DNL .war] implementados en el servidor de aplicaciones por los archivos incluidos con el servidor de implementación de referencia de acceso a Adobe.

Si planea utilizar el registro de dominios con el Servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Para volver a crear toda la base de datos de implementación de referencia, ejecute `CreateSampleDB.sql`. Para conservar los registros de base de datos existentes y agregar las nuevas tablas, abra `CreateSampleDB.sql`y ejecute solamente los comandos para crear las siguientes tablas:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Se deben agregar las siguientes propiedades a flashaccess-refimpl.properties para utilizar la compatibilidad con el dominio:

* `HandlerConfiguration.DomainCAs.n` o  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` y  `DomainRegistrationHandler.ServerCredential.password`, o  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Se deben agregar las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para admitir el envío de claves remotas a clientes de iOS:

* `HandlerConfiguration.KeyServerCertificate` o  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

