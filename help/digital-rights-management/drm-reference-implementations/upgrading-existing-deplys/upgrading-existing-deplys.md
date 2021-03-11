---
description: Para actualizar un servidor compatible con el servidor de licencias de implementación de referencia de la versión 3.0 o el paquete de carpetas vigiladas, debe reemplazar los archivos .war implementados en un servidor de aplicaciones por los archivos que se han incluido con el servidor de implementación de referencia de Adobe Primetime DRM.
title: Actualización de implementaciones existentes
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Información general {#upgrade-existing-deployments-overview}

Para actualizar un servidor compatible con el servidor de licencias de implementación de referencia de la versión 3.0 o el paquete de carpetas vigiladas, debe reemplazar los archivos .war implementados en un servidor de aplicaciones por los archivos que se han incluido con el servidor de implementación de referencia de Adobe Primetime DRM.

Para utilizar el registro de dominios con el servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Debe volver a crear toda la base de datos de implementación de referencia y ejecutar `CreateSampleDB.sql`.

Para conservar los registros de base de datos y agregar nuevas tablas:

1. Abra `CreateSampleDB.sql` y ejecute comandos que creen las siguientes tablas:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Agregue las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para utilizar la compatibilidad con el dominio:

   * `HandlerConfiguration.DomainCAs.n` o  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` y  `DomainRegistrationHandler.ServerCredential.password` o  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Agregue las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para admitir el envío de claves remotas a clientes de iOS:

   * `HandlerConfiguration.KeyServerCertificate` o  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`