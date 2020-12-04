---
seo-title: Actualización de implementaciones existentes
title: Actualización de implementaciones existentes
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Actualizando implementaciones existentes {#upgrading-existing-deployments}

Para actualizar un servidor que ejecute la versión 3.0 Reference Implementation License Server o Watched Folder Packager, reemplace los archivos [!DNL .war] implementados en el servidor de aplicaciones por los archivos incluidos con el servidor de implementación de referencia de Adobe Access.

Si planea utilizar el registro de dominio con el servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Para volver a crear toda la base de datos de implementación de referencia, ejecute `CreateSampleDB.sql`. Para conservar los registros de base de datos existentes y agregar las nuevas tablas, abra `CreateSampleDB.sql`y ejecute únicamente los comandos para crear las siguientes tablas:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Se deben agregar las siguientes propiedades a flashaccess-refimpl.properties para utilizar la compatibilidad con el dominio:

* `HandlerConfiguration.DomainCAs.n` o  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` y  `DomainRegistrationHandler.ServerCredential.password`, o  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Se deben agregar las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para admitir el envío de claves remotas en los clientes de iOS:

* `HandlerConfiguration.KeyServerCertificate` o  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

