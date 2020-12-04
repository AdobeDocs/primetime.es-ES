---
description: Gestión de la compatibilidad con FMRMS
seo-description: Gestión de la compatibilidad con FMRMS
seo-title: Actualización de clientes
title: Actualización de clientes
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Gestión de la compatibilidad con FMRMS {#handling-fmrms-compatibility}

Existen dos tipos de solicitudes relacionadas con la compatibilidad con Flash Media Rights Management Server 1.x. Se utiliza un tipo de solicitud para solicitar a los clientes 1.x que actualicen a un motor de ejecución que admita Adobe Primetime DRM 2.0 o posterior. Otro se utiliza para actualizar los metadatos 1.x al formato DRM Primetime antes de solicitar una licencia. Solo se necesita compatibilidad con estas solicitudes si previamente ha implementado contenido que utilice FMRMS 1.0 o 1.5.

## Actualizando clientes {#upgrading-clients}

Si un cliente FMRMS 1.x se pone en contacto con un servidor Adobe Primetime DRM, el servidor debe solicitar al cliente la actualización.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* La dirección URL de solicitud es &quot;*URL base desde contenido 1.x*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   A diferencia de otros controladores de solicitudes de Adobe Primetime, este controlador no proporciona acceso a ninguna información de solicitud ni requiere que se establezca ningún dato de respuesta. Cree una instancia de `FMRMSv1RequestHandler` y luego llame a `close()`

## Actualizando metadatos {#upgrading-metadata}

Si un cliente de Adobe Access encuentra contenido empaquetado con Flash Media Rights Management Server 1.x, extraerá los metadatos de codificación del contenido y los enviará al servidor. El servidor convertirá los metadatos de FMRMS 1.x al formato de Adobe Access y los enviará de nuevo al cliente. A continuación, el cliente envía los metadatos actualizados en una solicitud de licencia de Adobe Access estándar.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* La dirección URL de la solicitud es &quot;*URL base desde 1.x content*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

La conversión de metadatos se puede realizar sobre la marcha cuando el servidor recibe los metadatos antiguos del cliente. Como alternativa, el servidor podría preprocesar el contenido antiguo y almacenar los metadatos convertidos; en este caso, cuando el cliente solicita nuevos metadatos, el servidor solo necesita recuperar los nuevos metadatos que coincidan con el identificador de licencia de los metadatos antiguos.

Para convertir metadatos, el servidor debe realizar los siguientes pasos:

* Obtenga `LiveCycleKeyMetaData`. Para preconvertir los metadatos, `LiveCycleKeyMetaData` puede obtenerse de un archivo empaquetado con 1.x utilizando `MediaEncrypter.examineEncryptedContent()`. Los metadatos también se incluyen en la solicitud de conversión de metadatos ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenga el identificador de licencia de los metadatos antiguos y busque la clave y las directivas de cifrado (esta información se encontraba originalmente en la base de datos ES de Adobe LiveCycle. Las directivas ES de LiveCycle deben convertirse en directivas de Adobe Access 2.0). La implementación de referencia incluye secuencias de comandos y código de muestra para convertir las políticas y exportar información de licencias desde LiveCycle ES.
* Rellene el objeto `V2KeyParameters` (que recupera llamando a `MediaEncrypter.getKeyParameters()`).
* Cargue la `SigningCredential`, que es la credencial de empaquetador emitida por Adobe que se utiliza para firmar metadatos de codificación. Obtenga el objeto `SignatureParameters` llamando a `MediaEncrypter.getSignatureParameters()` y rellene la credencial de firma.
* Llame a `MetaDataConverter.convertMetadata()` para obtener el `V2ContentMetaData`.
* Llame a `V2ContentMetaData.getBytes()` y almacene para uso futuro, o llame a `FMRMSv1MetadataHandler.setUpdatedMetadata()`.