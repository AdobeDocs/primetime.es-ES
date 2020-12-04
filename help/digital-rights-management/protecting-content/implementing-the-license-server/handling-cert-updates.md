---
seo-title: Gestión de actualizaciones de certificados cuando caducan certificados emitidos por Adobes
title: Gestión de actualizaciones de certificados cuando caducan certificados emitidos por Adobes
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por Adobes{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Es posible que deba obtener un nuevo certificado de Adobe. Por ejemplo, un certificado de producción caduca cuando caduca un certificado de evaluación o cuando pasa de una evaluación a un certificado de producción. Siempre que un certificado caduque y no desee volver a empaquetar el contenido que utiliza el certificado antiguo, puede hacer que el servidor de licencias esté al tanto de los certificados antiguos como de los nuevos.

Para actualizar un servidor con nuevos certificados:

1. (Opcional) Cuando agregue nuevas entradas a una lista de actualización de directiva DRM o lista de revocación existente, deberá firmar con las nuevas credenciales y utilizar el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, puede utilizar la siguiente línea de comandos para agregar una entrada a una lista de actualización de directiva DRM existente, que se ha firmado con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Use la API de Java para actualizar el servidor de licencias con la nueva lista de actualización de directiva DRM o lista de revocación:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   o bien:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utiliza son `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. También debe actualizar el certificado que se utiliza para verificar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Si desea consumir contenido empaquetado con los certificados antiguos, asegúrese de que el servidor de licencias tiene acceso a las credenciales antiguas y nuevas del servidor de licencias, así como a las credenciales de transporte.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pasa al constructor `LicenseHandler`:

      * En la implementación de referencia, configúrela con la propiedad `LicenseHandler.ServerCredential`.
      * En el servidor DRM de Adobe Primetime para flujo protegido, la credencial actual debe ser la primera que se especifique en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales actuales y antiguas se proporcionan a `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela con las propiedades `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n`.

      * En Primetime DRM Server for Protected Streaming, las credenciales antiguas se especifican después de la primera credencial en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.

   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pasa al método `HandlerConfiguration.setServerTransportCredential()`:

      * En la implementación de referencia, configúrela con la propiedad `HandlerConfiguration.ServerTransportCredential`.
      * En Primetime DRM Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el elemento `TransportCredential` del archivo [!DNL flashaccess-tenant.xml].
   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela con las propiedades `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * En Primetime DRM Server para flujo protegido, esto se especifica después de la primera credencial en el elemento `TransportCredential` del archivo flashaccess-tenant.xml.




1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan contenido con las credenciales actuales. Asegúrese de que el certificado de servidor de licencias, el certificado de transporte y las credenciales de empaquetador más recientes se utilizan para empaquetar.
1. Actualice el certificado del servidor de licencias de Key Server de la siguiente manera:

   * Actualice las credenciales en el archivo de configuración del inquilino del servidor de claves DRM de Adobe Primetime incluyendo las credenciales antiguas y las nuevas del servidor de claves en flashaccess-keyserver-inquilino.xml.
   * Asegúrese de que el certificado actual se pasa al método `HandlerConfiguration.setKeyServerCertificate()`.

      * En la implementación de referencia, configúrela con la propiedad `HandlerConfiguration.KeyServerCertificate`.
      * En Primetime DRM Server para flujo protegido, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer.

