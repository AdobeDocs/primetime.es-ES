---
title: Actualización de metadatos
description: Actualización de metadatos
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Actualización de metadatos{#upgrading-metadata}

Si un cliente DRM de Adobe Primetime encuentra contenido empaquetado con Flash Media Rights Management Server 1.x, extrae los metadatos de cifrado del contenido y los envía al servidor. A continuación, el servidor convierte los metadatos de FMRMS 1.x al formato DRM de Primetime y los envía al cliente. A continuación, el cliente envía los metadatos actualizados en una solicitud de licencia DRM de Primetime estándar.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* La URL de solicitud es &quot;*URL base del contenido 1.x*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

La conversión de metadatos se podía realizar sobre la marcha cuando el servidor recibía los metadatos antiguos del cliente. Alternativamente, el servidor podría preprocesar el contenido antiguo y almacenar los metadatos convertidos; en este caso, cuando el cliente solicita nuevos metadatos, el servidor solo necesita recuperar los nuevos metadatos que coincidan con el identificador de licencia de los metadatos antiguos.

Para convertir metadatos, el servidor debe realizar los siguientes pasos:

* Obtener `LiveCycleKeyMetaData`. Para preconvertir los metadatos, `LiveCycleKeyMetaData` se puede obtener de un archivo empaquetado 1.x utilizando `MediaEncrypter.examineEncryptedContent()`. Los metadatos también se incluyen en la solicitud de conversión de metadatos ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Obtenga el identificador de licencia de los metadatos antiguos y busque la clave de cifrado y las políticas de DRM (esta información se encontraba originalmente en la base de datos del LiveCycle de Adobe ES). Las políticas de DRM de LiveCycle ES deben convertirse a políticas de DRM de Primetime 2.0). La Implementación de referencia incluye secuencias de comandos y código de ejemplo para convertir las directivas DRM y exportar la información de licencia desde LiveCycle ES.
* Rellene el `V2KeyParameters` objeto (que se recupera llamando a `MediaEncrypter.getKeyParameters()`).

* Cargue el `SigningCredential`, que es la credencial de empaquetador emitida por el Adobe que se utiliza para firmar metadatos de cifrado. Obtenga la `SignatureParameters` objeto llamando a `MediaEncrypter.getSignatureParameters()` y rellene la credencial de firma.

* Llamada `MetaDataConverter.convertMetadata()` para obtener la `V2ContentMetaData`.

* Llamada `V2ContentMetaData.getBytes()` y almacenar para uso futuro, o llamar a `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

