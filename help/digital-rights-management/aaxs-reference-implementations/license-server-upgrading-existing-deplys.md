---
seo-title: Actualización de implementaciones existentes
title: Actualización de implementaciones existentes
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Actualización de implementaciones existentes {#upgrading-existing-deployments}

Para actualizar un servidor que ejecute el servidor de licencias de implementación de referencia de la versión 3.0 o el empaquetador de carpetas vigiladas, sustituya los [!DNL .war] archivos implementados en el servidor de aplicaciones por los archivos incluidos con el servidor de implementación de referencia de Adobe Access.

Si planea utilizar el registro de dominio con el servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Para volver a crear toda la base de datos de implementación de referencia, ejecute `CreateSampleDB.sql`. Para conservar los registros de base de datos existentes y agregar las nuevas tablas, abra `CreateSampleDB.sql`y ejecute únicamente los comandos para crear las siguientes tablas:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Se deben agregar las siguientes propiedades a flashaccess-refimpl.properties para utilizar la compatibilidad con el dominio:

* `HandlerConfiguration.DomainCAs.n` o `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` y `DomainRegistrationHandler.ServerCredential.password`, o `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Se deben agregar las siguientes propiedades [!DNL flashaccess-refimpl.properties] para admitir la entrega remota de claves a los clientes de iOS:

* `HandlerConfiguration.KeyServerCertificate` o `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

