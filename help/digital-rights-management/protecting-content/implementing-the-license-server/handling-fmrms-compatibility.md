---
description: Gestión de la compatibilidad con FMRMS
title: Actualización de clientes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Gestión de la compatibilidad con FMRMS {#handling-fmrms-compatibility}

Existen dos tipos de solicitudes relacionadas con la compatibilidad con Flash Media Rights Management Server 1.x. Se utiliza un tipo de solicitud para solicitar a los clientes de 1.x que actualicen a un tiempo de ejecución que admita Adobe Primetime DRM 2.0 o posterior. Se utiliza otro para actualizar los metadatos 1.x al formato DRM de Primetime antes de poder solicitar una licencia. La compatibilidad con estas solicitudes solo es necesaria si ha implementado anteriormente contenido que utilice FMRMS 1.0 o 1.5.

## Actualización de clientes {#upgrading-clients}

Si un cliente de FMRMS 1.x se pone en contacto con un servidor DRM de Adobe Primetime, el servidor debe solicitar al cliente que actualice.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* La URL de solicitud es &quot;*URL base del contenido 1.x*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

  A diferencia de otros controladores de solicitudes de Adobe Primetime, este controlador no proporciona acceso a ninguna información de solicitud ni requiere que se establezcan datos de respuesta. Cree una instancia de `FMRMSv1RequestHandler`y, a continuación, invoque `close()`

## Actualización de metadatos {#upgrading-metadata}

Si un cliente de acceso a Adobe encuentra contenido empaquetado con Flash Media Rights Management Server 1.x, extraerá los metadatos de cifrado del contenido y los enviará al servidor. El servidor convertirá los metadatos de FMRMS 1.x al formato de acceso de Adobe y los devolverá al cliente. A continuación, el cliente envía los metadatos actualizados en una solicitud de licencia de acceso a Adobe estándar.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* La URL de solicitud es &quot;*URL base del contenido 1.x*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

La conversión de metadatos se podía realizar sobre la marcha cuando el servidor recibía los metadatos antiguos del cliente. Alternativamente, el servidor podría preprocesar el contenido antiguo y almacenar los metadatos convertidos; en este caso, cuando el cliente solicita nuevos metadatos, el servidor solo necesita recuperar los nuevos metadatos que coincidan con el identificador de licencia de los metadatos antiguos.

Para convertir metadatos, el servidor debe realizar los siguientes pasos:

* Obtener `LiveCycleKeyMetaData`. Para preconvertir los metadatos, `LiveCycleKeyMetaData` se puede obtener de un archivo empaquetado 1.x utilizando `MediaEncrypter.examineEncryptedContent()`. Los metadatos también se incluyen en la solicitud de conversión de metadatos ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenga el identificador de licencia de los metadatos antiguos y busque la clave de cifrado y las directivas (esta información se encontraba originalmente en la base de datos del LiveCycle de Adobe ES). Las directivas de LiveCycle ES deben convertirse en directivas de Adobe Access 2.0). La Implementación de referencia incluye secuencias de comandos y código de ejemplo para convertir las directivas y exportar la información de la licencia desde el LiveCycle ES.
* Rellene el `V2KeyParameters` objeto (que se recupera llamando a `MediaEncrypter.getKeyParameters()`).
* Cargue el `SigningCredential`, que es la credencial de empaquetador emitida por el Adobe que se utiliza para firmar metadatos de cifrado. Obtenga la `SignatureParameters` objeto llamando a `MediaEncrypter.getSignatureParameters()` y rellene la credencial de firma.
* Llamada `MetaDataConverter.convertMetadata()` para obtener la `V2ContentMetaData`.
* Llamada `V2ContentMetaData.getBytes()` y almacenar para uso futuro, o llamar a `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
