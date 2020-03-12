---
description: Para actualizar un servidor que admita la versión 3.0 Reference Implementation License Server o Watched Folder Packager, debe reemplazar los archivos .war implementados en un servidor de aplicaciones por los archivos incluidos con el servidor de implementación de referencia de Adobe Primetime DRM.
seo-description: Para actualizar un servidor que admita la versión 3.0 Reference Implementation License Server o Watched Folder Packager, debe reemplazar los archivos .war implementados en un servidor de aplicaciones por los archivos incluidos con el servidor de implementación de referencia de Adobe Primetime DRM.
seo-title: Actualizar implementaciones existentes
title: Actualizar implementaciones existentes
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Información general {#upgrade-existing-deployments-overview}

Para actualizar un servidor que admita la versión 3.0 Reference Implementation License Server o Watched Folder Packager, debe reemplazar los archivos .war implementados en un servidor de aplicaciones por los archivos incluidos con el servidor de implementación de referencia de Adobe Primetime DRM.

Para utilizar el registro de dominio con el servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Debe volver a crear toda la base de datos de implementación de referencia y ejecutar `CreateSampleDB.sql`.

Para conservar registros de base de datos y agregar nuevas tablas:

1. Abra `CreateSampleDB.sql` y ejecute comandos que creen las siguientes tablas:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Agregue las siguientes propiedades para [!DNL flashaccess-refimpl.properties] usar la compatibilidad con dominios:

   * `HandlerConfiguration.DomainCAs.n` o `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` y `DomainRegistrationHandler.ServerCredential.password` o `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Agregue las siguientes propiedades para [!DNL flashaccess-refimpl.properties] admitir la entrega remota de claves a los clientes de iOS:

   * `HandlerConfiguration.KeyServerCertificate` o `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`