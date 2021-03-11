---
title: Actualización de metadatos
description: Actualización de metadatos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Actualización de metadatos{#upgrading-metadata}

Si un cliente de acceso a Adobe encuentra contenido empaquetado con el Servidor 1.x de Media Rights Management de Flash, extraerá los metadatos de cifrado del contenido y los enviará al servidor. El servidor convierte los metadatos de FMRMS 1.x al formato de acceso al Adobe y los envía de nuevo al cliente. A continuación, el cliente envía los metadatos actualizados en una solicitud de licencia de acceso a Adobe estándar.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* La dirección URL de solicitud es &quot;*Dirección URL base desde 1.x content*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

La conversión de metadatos se puede realizar sobre la marcha cuando el servidor reciba los metadatos antiguos del cliente. Como alternativa, el servidor podría preprocesar el contenido antiguo y almacenar los metadatos convertidos; en este caso, cuando el cliente solicita nuevos metadatos, el servidor solo necesita recuperar los nuevos metadatos que coincidan con el identificador de licencia de los metadatos antiguos.

Para convertir metadatos, el servidor debe realizar los siguientes pasos:

* Obtenga `LiveCycleKeyMetaData`. Para convertir previamente los metadatos, `LiveCycleKeyMetaData` se puede obtener de un archivo 1.x empaquetado usando `MediaEncrypter.examineEncryptedContent()`. Los metadatos también se incluyen en la solicitud de conversión de metadatos ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenga el identificador de licencia de los metadatos antiguos y busque la clave y las directivas de cifrado (esta información se encontraba originalmente en la base de datos ES de Adobe LiveCycle. Las políticas de LiveCycle ES deben convertirse a directivas de acceso a Adobe 2.0). La Implementación de referencia incluye secuencias de comandos y código de muestra para convertir las políticas y exportar la información de licencia desde LiveCycle ES.
* Rellene el objeto `V2KeyParameters` (que se recupera llamando a `MediaEncrypter.getKeyParameters()`).
* Cargue el `SigningCredential`, que es la credencial del empaquetador emitida por el Adobe utilizado para firmar metadatos de codificación. Obtenga el objeto `SignatureParameters` llamando a `MediaEncrypter.getSignatureParameters()` y rellene la credencial de firma.
* Llame a `MetaDataConverter.convertMetadata()` para obtener el `V2ContentMetaData`.
* Llame a `V2ContentMetaData.getBytes()` y guarde para uso futuro, o llame a `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

