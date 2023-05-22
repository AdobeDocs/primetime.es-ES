---
description: Para actualizar un servidor que admita el servidor de licencias de implementación de referencia de la versión 3.0 o el empaquetador de carpetas inspeccionadas, debe reemplazar los archivos .war que se han implementado en un servidor de aplicaciones por los archivos que se han incluido con el servidor de implementación de referencia de Adobe Primetime DRM.
title: Actualización de implementaciones existentes
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Información general {#upgrade-existing-deployments-overview}

Para actualizar un servidor que admita el servidor de licencias de implementación de referencia de la versión 3.0 o el empaquetador de carpetas inspeccionadas, debe reemplazar los archivos .war que se han implementado en un servidor de aplicaciones por los archivos que se han incluido con el servidor de implementación de referencia de Adobe Primetime DRM.

Para utilizar el registro de dominios con el servidor de licencias de implementación de referencia, se requieren varias tablas de base de datos nuevas. Debe volver a crear toda la base de datos de implementación de referencia y ejecutar `CreateSampleDB.sql`.

Para conservar los registros de la base de datos y agregar nuevas tablas:

1. Abrir `CreateSampleDB.sql` y ejecute comandos que creen las tablas siguientes:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Agregue las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para usar la compatibilidad con el dominio:

   * `HandlerConfiguration.DomainCAs.n` o `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` y `DomainRegistrationHandler.ServerCredential.password` o `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Agregue las siguientes propiedades a [!DNL flashaccess-refimpl.properties] para admitir la entrega de claves remotas a clientes de iOS:

   * `HandlerConfiguration.KeyServerCertificate` o `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
