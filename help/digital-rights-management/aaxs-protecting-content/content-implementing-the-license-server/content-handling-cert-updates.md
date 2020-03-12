---
seo-title: Gestión de actualizaciones de certificados cuando caduquen los certificados emitidos por Adobe
title: Gestión de actualizaciones de certificados cuando caduquen los certificados emitidos por Adobe
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestión de actualizaciones de certificados cuando caduquen los certificados emitidos por Adobe {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Es posible que en ocasiones tenga que obtener un nuevo certificado de Adobe. Por ejemplo, cuando caduca un certificado de producción, caduca un certificado de evaluación o cuando pasa de una evaluación a un certificado de producción. Cuando caduca un certificado y no desea volver a empaquetar el contenido que utilizó el certificado antiguo. Puede hacer que el servidor de licencias esté al tanto de los certificados antiguos como de los nuevos.

Siga el procedimiento siguiente para actualizar el servidor con los nuevos certificados:

1. (Opcional) Al agregar nuevas entradas a una lista de revocación o actualización de directiva existente, asegúrese de firmar con las nuevas credenciales y utilizar el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, utilice la siguiente línea de comandos para agregar una entrada a una lista de actualización de directiva existente, que se firmó con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilice la API de Java para actualizar el servidor de licencias con la nueva lista de actualizaciones de directivas o de revocación:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   o bien:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utilice son `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. Actualice también el certificado utilizado para verificar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir contenido empaquetado con los certificados antiguos, el servidor de licencias necesita las credenciales antiguas y nuevas del servidor de licencias y las credenciales de transporte. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pasa al `LicenseHandler` constructor:

      * En la implementación de referencia, configúrela mediante la `LicenseHandler.ServerCredential` propiedad .
      * En Adobe Access Server for Protected Streaming, la credencial actual debe ser la primera credencial especificada en el `LicenseServerCredential` elemento del archivo flashaccess-tenant.xml.
   * Asegúrese de que se proporcionan las credenciales actuales y antiguas a `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela a través de las propiedades `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n` .
      * En Adobe Access Server for Protected Streaming, las credenciales antiguas se especifican después de la primera credencial del `LicenseServerCredential` elemento en el archivo flashaccess-tenant.xml.
   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pasa al `HandlerConfiguration.setServerTransportCredential()` método:

      * En la implementación de referencia, configúrela mediante la `HandlerConfiguration.ServerTransportCredential` propiedad .
      * En Adobe Access Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el `TransportCredential` elemento del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela a través de las `HandlerConfiguration.AdditionalServerTransportCredential. n` propiedades.
      * En Adobe Access Server para flujo protegido, esto se especifica después de la primera credencial del `TransportCredential` elemento en el archivo flashaccess-tenant.xml.




1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan contenido con las credenciales actuales. Asegúrese de que el certificado de servidor de licencias, el certificado de transporte y las credenciales de empaquetador más recientes se utilizan para empaquetar.
1. Para actualizar el certificado del servidor de licencias de Key Server:

   * Actualice las credenciales en el archivo de configuración del inquilino del servidor de claves de Adobe Access. Incluya las credenciales antiguas y las nuevas del servidor clave en flashaccess-keyserver-inquilino.xml.
   * Asegúrese de que el certificado actual se pasa al `HandlerConfiguration.setKeyServerCertificate()` método.

      * En la implementación de referencia, configúrela mediante la `HandlerConfiguration.KeyServerCertificate` propiedad .
      * En Adobe Access Server for Protected Streaming, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer.

