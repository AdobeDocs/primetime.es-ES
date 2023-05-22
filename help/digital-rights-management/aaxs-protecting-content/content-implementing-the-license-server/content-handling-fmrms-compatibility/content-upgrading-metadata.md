---
title: Actualización de metadatos
description: Actualización de metadatos
copied-description: true
exl-id: 04b3fb22-489e-41bb-95d0-99375f92fbae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Actualización de metadatos{#upgrading-metadata}

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
