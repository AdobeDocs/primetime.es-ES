---
title: Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe
description: Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Es posible que deba obtener un nuevo certificado del Adobe. Por ejemplo, un certificado de producción caduca cuando caduca un certificado de evaluación o cuando cambia de una evaluación a un certificado de producción. Siempre que un certificado caduque y no desee volver a empaquetar el contenido que utiliza el certificado antiguo, puede hacer que el servidor de licencias tenga en cuenta tanto el certificado antiguo como el nuevo.

Para actualizar un servidor con certificados nuevos:

1. (Opcional) Cuando se añaden nuevas entradas a una lista de actualización o de revocación de directivas DRM existente, es necesario firmar con las nuevas credenciales y utilizar el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, puede utilizar la siguiente línea de comandos para añadir una entrada a una lista de actualización de directivas de DRM existente, que se ha firmado con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Utilice la API de Java para actualizar el servidor de licencias con la nueva lista de actualización o la lista de revocación de la directiva DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   o:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utiliza son las siguientes `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. También debe actualizar el certificado que se utiliza para comprobar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Si desea consumir contenido que se haya empaquetado utilizando los certificados antiguos, asegúrese de que el servidor de licencias tiene acceso a las credenciales del servidor de licencias antiguo y nuevo, así como a las credenciales de transporte.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pase al `LicenseHandler` constructor:

      * En la implementación de referencia, configúrela con el `LicenseHandler.ServerCredential` propiedad.
      * En el servidor DRM de Adobe Primetime para flujo protegido, la credencial actual debe ser la primera que se especifique en la variable `LicenseServerCredential` en el archivo flashaccess-tenant.xml.

   * Asegúrese de que las credenciales actuales y antiguas se proporcionan a `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela con el `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n` propiedades.

      * En el servidor DRM de Primetime para flujo protegido, las credenciales antiguas se especifican después de la primera credencial en el `LicenseServerCredential` en el archivo flashaccess-tenant.xml.

   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pase al `HandlerConfiguration.setServerTransportCredential()` método:

      * En la implementación de referencia, configúrela con el `HandlerConfiguration.ServerTransportCredential` propiedad.
      * En el servidor DRM de Primetime para el streaming protegido, la credencial actual debe ser la primera credencial especificada en la variable `TransportCredential` elemento en el [!DNL flashaccess-tenant.xml] archivo.

   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela con el `HandlerConfiguration.AdditionalServerTransportCredential. n` propiedades.
      * En el servidor DRM de Primetime para flujo continuo protegido, esto se especifica después de la primera credencial en la `TransportCredential` en el archivo flashaccess-tenant.xml.

1. Actualice las herramientas de empaquetado para asegurarse de que están empaquetando el contenido con las credenciales actuales. Asegúrese de que se utilizan el certificado de servidor de licencias, el certificado de transporte y las credenciales del empaquetador más recientes para el empaquetado.
1. Actualice el certificado del servidor de licencias del servidor de claves de la siguiente manera:

   * Actualice las credenciales en el archivo de configuración del inquilino del servidor de claves DRM de Adobe Primetime incluyendo las credenciales antiguas y nuevas del servidor de claves en flashaccess-keyserver-tenant.xml.
   * Asegúrese de que el certificado actual se pasa al `HandlerConfiguration.setKeyServerCertificate()` método.

      * En la implementación de referencia, configúrela con el `HandlerConfiguration.KeyServerCertificate` propiedad.
      * En el servidor DRM de Primetime para flujo protegido, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer.
