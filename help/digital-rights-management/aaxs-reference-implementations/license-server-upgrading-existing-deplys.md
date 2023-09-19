---
title: Actualización de implementaciones existentes
description: Actualización de implementaciones existentes
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Actualización de implementaciones existentes {#upgrading-existing-deployments}

Para actualizar un servidor que ejecute el servidor de licencias de implementación de referencia de la versión 3.0 o el empaquetador de carpetas inspeccionadas, reemplace el [!DNL .war] archivos implementados en el servidor de aplicaciones con los archivos incluidos en el servidor de implementación de referencia de acceso a Adobe.

Si planea utilizar el registro de dominios con el servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Para volver a crear toda la base de datos de implementación de referencia, ejecute `CreateSampleDB.sql`. Para conservar los registros de base de datos existentes y agregar las nuevas tablas, abra `CreateSampleDB.sql`y ejecute únicamente los comandos para crear las tablas siguientes:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Se deben agregar las siguientes propiedades a flashaccess-refimpl.properties para utilizar la compatibilidad con el dominio:

* `HandlerConfiguration.DomainCAs.n` o `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` y `DomainRegistrationHandler.ServerCredential.password`, o `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Se deben añadir las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para admitir la entrega de claves remotas a clientes de iOS:

* `HandlerConfiguration.KeyServerCertificate` o `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
