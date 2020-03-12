---
seo-title: Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por Adobe
title: Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por Adobe
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por Adobe{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Es posible que deba obtener un nuevo certificado de Adobe. Por ejemplo, un certificado de producción caduca cuando caduca un certificado de evaluación o cuando pasa de una evaluación a un certificado de producción. Siempre que un certificado caduque y no desee volver a empaquetar el contenido que utiliza el certificado antiguo, puede hacer que el servidor de licencias esté al tanto de los certificados antiguos como de los nuevos.

Para actualizar un servidor con nuevos certificados:

1. (Opcional) Cuando agregue nuevas entradas a una lista de revocación o actualización de directiva DRM existente, deberá firmar con las nuevas credenciales y utilizar el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, puede utilizar la siguiente línea de comandos para agregar una entrada a una lista de actualización de directivas DRM existente, que se ha firmado con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Use la API de Java para actualizar el servidor de licencias con la nueva lista de actualizaciones de directivas de DRM o lista de revocación:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   o bien:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que se utilizan son `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. También debe actualizar el certificado que se utiliza para verificar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Si desea consumir contenido empaquetado con los certificados antiguos, asegúrese de que el servidor de licencias tiene acceso a las credenciales antiguas y nuevas del servidor de licencias, así como a las credenciales de transporte.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pasa al `LicenseHandler` constructor:

      * En la implementación de referencia, configúrela con la `LicenseHandler.ServerCredential` propiedad .
      * En Adobe Primetime DRM Server for Protected Streaming, la credencial actual debe ser la primera credencial especificada en el `LicenseServerCredential` elemento del archivo flashaccess-tenant.xml.
   * Asegúrese de que se proporcionan las credenciales actuales y antiguas a `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela con las propiedades `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n` .

      * En Primetime DRM Server for Protected Streaming, las credenciales antiguas se especifican después de la primera credencial del `LicenseServerCredential` elemento en el archivo flashaccess-tenant.xml.
   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pasa al `HandlerConfiguration.setServerTransportCredential()` método:

      * En la implementación de referencia, configúrela con la `HandlerConfiguration.ServerTransportCredential` propiedad .
      * En Primetime DRM Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el `TransportCredential` elemento del [!DNL flashaccess-tenant.xml] archivo.
   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela con las `HandlerConfiguration.AdditionalServerTransportCredential. n` propiedades.
      * En Primetime DRM Server para flujo protegido, esto se especifica después de la primera credencial del `TransportCredential` elemento en el archivo flashaccess-tenant.xml.




1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan contenido con las credenciales actuales. Asegúrese de que el certificado de servidor de licencias, el certificado de transporte y las credenciales de empaquetador más recientes se utilizan para empaquetar.
1. Actualice el certificado del servidor de licencias de Key Server de la siguiente manera:

   * Actualice las credenciales en el archivo de configuración del inquilino de Adobe Primetime DRM Key Server incluyendo tanto las credenciales antiguas como las nuevas en flashaccess-keyserver-inquilino.xml.
   * Asegúrese de que el certificado actual se pasa al `HandlerConfiguration.setKeyServerCertificate()` método.

      * En la implementación de referencia, configúrela con la `HandlerConfiguration.KeyServerCertificate` propiedad .
      * En Primetime DRM Server para flujo protegido, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer.

