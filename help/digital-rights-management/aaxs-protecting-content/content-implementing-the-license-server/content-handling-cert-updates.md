---
title: Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe
description: Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Puede haber ocasiones en las que tenga que obtener un nuevo certificado del Adobe. Por ejemplo, cuando caduca un certificado de producción, caduca un certificado de evaluación o cuando cambia de una evaluación a un certificado de producción. Cuando caduca un certificado y no desea volver a empaquetar el contenido que utilizó el certificado antiguo. Puede hacer que el servidor de licencias tenga en cuenta tanto los certificados antiguos como los nuevos.

Utilice el siguiente procedimiento para actualizar el servidor con los nuevos certificados:

1. (Opcional) Cuando agregue nuevas entradas a una lista de actualización o revocación de directivas existente, asegúrese de firmar con las nuevas credenciales y utilice el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, utilice la siguiente línea de comandos para agregar una entrada a una lista de actualización de directivas existente, que se firmó con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilice la API de Java para actualizar el servidor de licencias con la nueva lista de actualización de directivas o la lista de revocación:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   o:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utiliza son las siguientes `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. Actualice también el certificado utilizado para comprobar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir contenido empaquetado con los certificados antiguos, el servidor de licencias necesita las credenciales del servidor de licencias antiguo y nuevo, así como las credenciales de transporte. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pase al `LicenseHandler` constructor:

      * En la implementación de referencia, configúrela a través de `LicenseHandler.ServerCredential` propiedad.
      * En Adobe Access Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en la variable `LicenseServerCredential` en el archivo flashaccess-tenant.xml.

   * Asegúrese de que las credenciales actuales y antiguas se proporcionan a `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela a través de `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n` propiedades.
      * En Adobe Access Server para flujo protegido, las credenciales antiguas se especifican después de la primera credencial de la `LicenseServerCredential` en el archivo flashaccess-tenant.xml.

   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pase al `HandlerConfiguration.setServerTransportCredential()` método:

      * En la implementación de referencia, configúrela a través de `HandlerConfiguration.ServerTransportCredential` propiedad.
      * En Adobe Access Server para el streaming protegido, la credencial actual debe ser la primera especificada en la variable `TransportCredential` en el archivo flashaccess-tenant.xml.

   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela a través de `HandlerConfiguration.AdditionalServerTransportCredential. n` propiedades.
      * En Adobe Access Server para flujo continuo protegido, esto se especifica después de la primera credencial en la `TransportCredential` en el archivo flashaccess-tenant.xml.

1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan el contenido con las credenciales actuales. Asegúrese de que se utilizan el certificado de servidor de licencias, el certificado de transporte y las credenciales del empaquetador más recientes para el empaquetado.
1. Para actualizar el certificado del servidor de licencias del servidor de claves:

   * Actualice las credenciales en el archivo de configuración del inquilino del servidor de claves de acceso a Adobe. Incluya las credenciales antiguas y nuevas del servidor de claves en flashaccess-keyserver-tenant.xml.
   * Asegúrese de que el certificado actual se pasa a `HandlerConfiguration.setKeyServerCertificate()` método.

      * En la implementación de referencia, configúrela a través de `HandlerConfiguration.KeyServerCertificate` propiedad.
      * En Adobe Access Server para flujo protegido, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer.
