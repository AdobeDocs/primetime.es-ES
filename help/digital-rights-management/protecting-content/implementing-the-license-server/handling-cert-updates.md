---
title: Gestión de actualizaciones de certificados cuando expiren los certificados emitidos por Adobe
description: Gestión de actualizaciones de certificados cuando expiren los certificados emitidos por Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Gestión de actualizaciones de certificados cuando expiren los certificados emitidos por el Adobe{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Es posible que deba obtener un nuevo certificado de Adobe. Por ejemplo, un certificado de producción caduca cuando caduca un certificado de evaluación o cuando cambia de una evaluación a un certificado de producción. Siempre que un certificado caduque y no desee volver a empaquetar el contenido que utiliza el certificado antiguo, puede hacer que el servidor de licencias tenga en cuenta tanto los certificados antiguos como los nuevos.

Para actualizar un servidor con nuevos certificados:

1. (Opcional) Cuando agregue nuevas entradas a una lista de revocación o lista de actualización de directivas de DRM existente, deberá firmar con las nuevas credenciales y utilizar el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, puede utilizar la siguiente línea de comandos para agregar una entrada a una lista existente de actualización de directivas de DRM, que se ha firmado con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Utilice la API de Java para actualizar el servidor de licencias con la nueva lista de actualización o lista de revocación de directivas de DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   o:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utiliza son `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. También debe actualizar el certificado que se utiliza para verificar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Si desea consumir contenido que se haya empaquetado con certificados antiguos, asegúrese de que el servidor de licencias tenga acceso a las credenciales antiguas y nuevas del servidor de licencias, así como a las credenciales de transporte.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pasa al constructor `LicenseHandler`:

      * En la implementación de referencia, configúrela con la propiedad `LicenseHandler.ServerCredential` .
      * En el servidor DRM de Adobe Primetime para transmisión protegida, la credencial actual debe ser la primera credencial que se especifique en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales actuales y antiguas se proporcionan en `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela con las propiedades `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n` .

      * En Primetime DRM Server para transmisión protegida, las credenciales antiguas se especifican después de la primera credencial en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.

   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pase al método `HandlerConfiguration.setServerTransportCredential()`:

      * En la implementación de referencia, configúrela con la propiedad `HandlerConfiguration.ServerTransportCredential` .
      * En Primetime DRM Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el elemento `TransportCredential` del archivo [!DNL flashaccess-tenant.xml].
   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela con las propiedades `HandlerConfiguration.AdditionalServerTransportCredential. n` .
      * En Primetime DRM Server para flujo protegido, esto se especifica después de la primera credencial en el elemento `TransportCredential` en el archivo flashaccess-tenant.xml.




1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan contenido con las credenciales actuales. Asegúrese de que el certificado de servidor de licencias, el certificado de transporte y las credenciales del empaquetador más recientes se utilizan para el empaquetado.
1. Actualice el certificado del servidor de licencias de Key Server de la siguiente manera:

   * Actualice las credenciales en el archivo de configuración del inquilino del servidor de claves DRM de Adobe Primetime incluyendo las credenciales antiguas y nuevas del servidor de claves en flashaccess-keyserver-tenant.xml.
   * Asegúrese de que el certificado actual se pasa al método `HandlerConfiguration.setKeyServerCertificate()` .

      * En la implementación de referencia, configúrela con la propiedad `HandlerConfiguration.KeyServerCertificate` .
      * En Servidor de DRM de Primetime para transmisión protegida, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer .

