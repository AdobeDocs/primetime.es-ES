---
seo-title: Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por Adobes
title: Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por Adobes
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Es posible que haya ocasiones en las que tenga que obtener un nuevo certificado de Adobe. Por ejemplo, cuando caduca un certificado de producción, caduca un certificado de evaluación o cuando pasa de una evaluación a un certificado de producción. Cuando caduca un certificado y no desea volver a empaquetar el contenido que utilizó el certificado antiguo. Puede hacer que el servidor de licencias esté al tanto de los certificados antiguos como de los nuevos.

Siga el procedimiento siguiente para actualizar el servidor con los nuevos certificados:

1. (Opcional) Al agregar nuevas entradas a una lista de actualización de directiva o lista de revocación existente, asegúrese de firmar con las nuevas credenciales y utilizar el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, utilice la siguiente línea de comandos para agregar una entrada a una lista de actualización de directiva existente, que se firmó con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilice la API de Java para actualizar el servidor de licencias con la nueva lista de actualización de directiva o lista de revocación:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   o bien:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utiliza son `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. Actualice también el certificado utilizado para verificar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir contenido empaquetado con los certificados antiguos, el servidor de licencias necesita las credenciales antiguas y nuevas del servidor de licencias y las credenciales de transporte. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pasa al constructor `LicenseHandler`:

      * En la implementación de referencia, configúrela mediante la propiedad `LicenseHandler.ServerCredential`.
      * En Adobe Access Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales actuales y antiguas se proporcionan a `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela a través de las propiedades `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n`.
      * En Adobe Access Server para flujo protegido, las credenciales antiguas se especifican después de la primera credencial en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.

   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pasa al método `HandlerConfiguration.setServerTransportCredential()`:

      * En la implementación de referencia, configúrela mediante la propiedad `HandlerConfiguration.ServerTransportCredential`.
      * En Adobe Access Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el elemento `TransportCredential` del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela a través de las propiedades `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * En Adobe Access Server para flujo protegido, esto se especifica después de la primera credencial del elemento `TransportCredential` en el archivo flashaccess-tenant.xml.




1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan contenido con las credenciales actuales. Asegúrese de que el certificado de servidor de licencias, el certificado de transporte y las credenciales de empaquetador más recientes se utilizan para empaquetar.
1. Para actualizar el certificado del servidor de licencias de Key Server:

   * Actualice las credenciales en el archivo de configuración del inquilino de Adobe Access Key Server. Incluya las credenciales antiguas y las nuevas del servidor clave en flashaccess-keyserver-inquilino.xml.
   * Asegúrese de que el certificado actual se pasa al método `HandlerConfiguration.setKeyServerCertificate()`.

      * En la implementación de referencia, configúrela mediante la propiedad `HandlerConfiguration.KeyServerCertificate`.
      * En Adobe Access Server para flujo protegido, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer.

