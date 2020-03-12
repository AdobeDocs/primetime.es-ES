---
seo-title: Actualización de metadatos
title: Actualización de metadatos
uuid: cad0b23e-50ca-47ae-871f-be571cb00a26
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Actualización de metadatos{#upgrading-metadata}

Si un cliente de Adobe Access encuentra contenido empaquetado con Flash Media Rights Management Server 1.x, extraerá los metadatos de codificación del contenido y los enviará al servidor. El servidor convertirá los metadatos de FMRMS 1.x al formato de Adobe Access y los enviará al cliente. A continuación, el cliente envía los metadatos actualizados en una solicitud de licencia estándar de Adobe Access.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* La dirección URL de la solicitud es &quot;URL *base desde contenido* 1.x&quot; +&quot;/flashaccess/header erconversion/v1&quot;.

La conversión de metadatos se puede realizar sobre la marcha cuando el servidor recibe los metadatos antiguos del cliente. Como alternativa, el servidor podría preprocesar el contenido antiguo y almacenar los metadatos convertidos; en este caso, cuando el cliente solicita nuevos metadatos, el servidor solo necesita recuperar los nuevos metadatos que coincidan con el identificador de licencia de los metadatos antiguos.

Para convertir metadatos, el servidor debe realizar los siguientes pasos:

* Ve `LiveCycleKeyMetaData`. Para convertir previamente los metadatos, `LiveCycleKeyMetaData` puede obtenerse de un archivo empaquetado con 1.x mediante `MediaEncrypter.examineEncryptedContent()`. Los metadatos también se incluyen en la solicitud de conversión de metadatos ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenga el identificador de licencia de los metadatos antiguos y busque la clave y las políticas de codificación (esta información se encontraba originalmente en la base de datos de Adobe LiveCycle ES. Las directivas de LiveCycle ES deben convertirse a políticas de Adobe Access 2.0). La implementación de referencia incluye secuencias de comandos y código de muestra para convertir las políticas y exportar información de licencias desde LiveCycle ES.
* Rellene el `V2KeyParameters` objeto (que se recupera llamando a `MediaEncrypter.getKeyParameters()`).
* Cargue la `SigningCredential`, que es la credencial de empaquetador emitida por Adobe que se utiliza para firmar metadatos de codificación. Obtenga el `SignatureParameters` objeto llamando `MediaEncrypter.getSignatureParameters()` y rellene la credencial de firma.
* Llame `MetaDataConverter.convertMetadata()` para obtener el `V2ContentMetaData`.
* Llame `V2ContentMetaData.getBytes()` y almacene para uso futuro o llame a `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

