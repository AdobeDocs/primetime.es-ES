---
title: Gestión de actualizaciones de certificados cuando expiren los certificados emitidos por el Adobe
description: Gestión de actualizaciones de certificados cuando expiren los certificados emitidos por el Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Gestión de actualizaciones de certificados cuando expiren los certificados emitidos por el Adobe {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Puede haber ocasiones en las que tenga que obtener un nuevo certificado de Adobe. Por ejemplo, cuando caduca un certificado de producción, caduca un certificado de evaluación o cuando pasa de una evaluación a un certificado de producción. Cuando caduca un certificado y no desea volver a empaquetar el contenido que usaba el certificado antiguo. Puede hacer que el servidor de licencias tenga en cuenta tanto los certificados antiguos como los nuevos.

Utilice el siguiente procedimiento para actualizar el servidor con los nuevos certificados:

1. (Opcional) Cuando agregue nuevas entradas a una lista de revocación o una lista de actualización de directivas existente, asegúrese de firmar con las nuevas credenciales y utilice el certificado antiguo para validar la firma en el archivo existente.

   Por ejemplo, utilice la siguiente línea de comandos para agregar una entrada a una lista de actualización de directivas existente, que se firmó con una credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilice la API de Java para actualizar el servidor de licencias con la nueva lista de actualización o lista de revocación de directivas:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   o:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   En la implementación de referencia, las propiedades que utiliza son `HandlerConfiguration.RevocationList` y `HandlerConfiguration.PolicyUpdateList`. Actualice también el certificado utilizado para verificar las firmas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir contenido empaquetado con certificados antiguos, el servidor de licencias requiere las credenciales antiguas y nuevas del servidor de licencias y las credenciales de transporte. Actualice el servidor de licencias con los certificados nuevos y antiguos.

   Para las credenciales del servidor de licencias:

   * Asegúrese de que la credencial actual se pasa al constructor `LicenseHandler`:

      * En la implementación de referencia, configúrela a través de la propiedad `LicenseHandler.ServerCredential` .
      * En Adobe Access Server para la transmisión protegida, la credencial actual debe ser la primera credencial especificada en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales actuales y antiguas se proporcionan en `AsymmetricKeyRetrieval`

      * En la implementación de referencia, configúrela a través de las propiedades `LicenseHandler.ServerCredential` y `AsymmetricKeyRetrieval.ServerCredential. n` .
      * En Adobe Access Server para la transmisión protegida, las credenciales antiguas se especifican después de la primera credencial en el elemento `LicenseServerCredential` del archivo flashaccess-tenant.xml.

   Para las credenciales de transporte:

   * Asegúrese de que la credencial actual se pase al método `HandlerConfiguration.setServerTransportCredential()`:

      * En la implementación de referencia, configúrela a través de la propiedad `HandlerConfiguration.ServerTransportCredential` .
      * En Adobe Access Server para flujo protegido, la credencial actual debe ser la primera credencial especificada en el elemento `TransportCredential` del archivo flashaccess-tenant.xml.
   * Asegúrese de que las credenciales antiguas se proporcionan a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * En la implementación de referencia, configúrela a través de las propiedades `HandlerConfiguration.AdditionalServerTransportCredential. n` .
      * En Adobe Access Server para flujo protegido, esto se especifica después de la primera credencial en el elemento `TransportCredential` del archivo flashaccess-tenant.xml.




1. Actualice las herramientas de empaquetado para asegurarse de que empaquetan contenido con las credenciales actuales. Asegúrese de que el certificado de servidor de licencias, el certificado de transporte y las credenciales del empaquetador más recientes se utilizan para el empaquetado.
1. Para actualizar el certificado de servidor de licencias del servidor clave:

   * Actualice las credenciales en el archivo de configuración del inquilino del servidor de claves de acceso a Adobe. Incluya las credenciales antiguas y nuevas de Key Server en flashaccess-keyserver-tenant.xml.
   * Asegúrese de que el certificado actual se pasa al método `HandlerConfiguration.setKeyServerCertificate()` .

      * En la implementación de referencia, configúrela a través de la propiedad `HandlerConfiguration.KeyServerCertificate` .
      * En Adobe Access Server para la transmisión protegida, especifique el certificado del servidor de claves en mediante el elemento Configuration/Tenant/Certificates/KeyServer .

