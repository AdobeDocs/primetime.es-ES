---
seo-title: Actualización de metadatos
title: Actualización de metadatos
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Actualización de metadatos{#upgrading-metadata}

Si un cliente DRM de Adobe Primetime encuentra contenido empaquetado con Flash Media Rights Management Server 1.x, extrae los metadatos de codificación del contenido y los envía al servidor. A continuación, el servidor convierte los metadatos de FMRMS 1.x al formato DRM Primetime y los envía al cliente. A continuación, el cliente envía los metadatos actualizados en una solicitud de licencia de Primetime DRM estándar.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* La dirección URL de la solicitud es &quot;URL *base del contenido* de 1.x&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

La conversión de metadatos se puede realizar sobre la marcha cuando el servidor recibe los metadatos antiguos del cliente. Como alternativa, el servidor podría preprocesar el contenido antiguo y almacenar los metadatos convertidos; en este caso, cuando el cliente solicita nuevos metadatos, el servidor solo necesita recuperar los nuevos metadatos que coincidan con el identificador de licencia de los metadatos antiguos.

Para convertir metadatos, el servidor debe realizar los siguientes pasos:

* Ve `LiveCycleKeyMetaData`. Para convertir previamente los metadatos, `LiveCycleKeyMetaData` puede obtenerse de un archivo empaquetado con 1.x mediante `MediaEncrypter.examineEncryptedContent()`. Los metadatos también se incluyen en la solicitud de conversión de metadatos ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Obtenga el identificador de licencia de los metadatos antiguos y busque la clave de cifrado y las directivas DRM (esta información se encontraba originalmente en la base de datos de Adobe LiveCycle ES. Las políticas de DRM de LiveCycle ES deben convertirse a políticas de DRM de Primetime 2.0). La implementación de referencia incluye secuencias de comandos y código de muestra para convertir las políticas de DRM y exportar información de licencias desde LiveCycle ES.
* Rellene el `V2KeyParameters` objeto (que se recupera llamando a `MediaEncrypter.getKeyParameters()`).

* Cargue la `SigningCredential`, que es la credencial de empaquetador emitida por Adobe que se utiliza para firmar metadatos de codificación. Obtenga el `SignatureParameters` objeto llamando `MediaEncrypter.getSignatureParameters()` y rellene la credencial de firma.

* Llame `MetaDataConverter.convertMetadata()` para obtener el `V2ContentMetaData`.

* Llame `V2ContentMetaData.getBytes()` y almacene para uso futuro o llame a `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

