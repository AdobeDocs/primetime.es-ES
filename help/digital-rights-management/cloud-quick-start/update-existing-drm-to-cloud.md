---
title: Actualizar contenido DRM existente para utilizar DRM de la nube (opcional)
description: Actualizar contenido DRM existente para utilizar DRM de la nube (opcional)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Actualizar contenido DRM existente para utilizar DRM de la nube (opcional) {#update-existing-drm-content-to-use-cloud-drm-optional}

Si tiene una biblioteca de contenido existente protegida por Primetime DRM, es posible &quot;volver a encabezado&quot; el contenido existente para utilizar el servicio DRM de Primetime Cloud, en lugar de tener que volver a empaquetar/cifrar los archivos de origen originales. Volver a enviar el contenido simplemente actualiza los metadatos DRM del contenido en el manifiesto HLS. No realiza ninguna operación de descifrado/recifrado del recurso original. Esta puede ser una opción útil si el contenido de origen original no está disponible o si existe preocupación por la cantidad de recursos necesarios para volver a empaquetar una biblioteca grande.

Es posible utilizar el SDK de Java de DRM de Primetime para actualizar los metadatos mediante programación. Además, la variable [!DNL OfflinePackager.jar] La herramienta de línea de comandos incluida con este kit de protección también puede realizar esta tarea utilizando `-drm_refresh` opción.

## Detalles sobre volver a encabezado {#section_3F3980D8E775450588C64E02A8448189}

Para utilizar CloudDRM, es necesario actualizar los siguientes campos:

* URL del servidor de licencias (para [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificado del servidor de licencias (al certificado del servidor de licencias CloudDRM)
* Certificado de transporte (al certificado de transporte CloudDRM)
* Credencial del empaquetador (a la credencial del empaquetador que ha activado para su uso con CloudDRM)

## Búsqueda de metadatos DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

El contenido que utiliza tecnología HTTP (como HDS o HLS) utiliza un manifiesto que hace referencia a los metadatos DRM de acceso de Adobe. En el HDS, el sistema hace referencia a los metadatos `<drmmeta>` y, en HLS, la etiqueta hace referencia a ella el `#EXT-X-FAXS-CM` etiqueta. En cualquier escenario, los metadatos se pueden contener en línea en el manifiesto como un blob codificado en base 64 o se puede hacer referencia externamente como un archivo binario. Si los metadatos están incrustados/en línea en el manifiesto, es posible que tenga que descodificar primero en base64 los metadatos en datos binarios antes de utilizar esos datos para crear una instancia de los metadatos DRM.

## Uso del archivo OfflinePackage.jar incluido {#section_37C2091856E44AA380D742C72B4DD1A7}

Proporcione el `-drm_refresh option` a la línea de comandos. Se creará un nuevo archivo de manifiesto con metadatos DRM actualizados, mientras que el contenido no se volverá a cifrar.

## Uso del SDK de Java de Primetime DRM para volver a enviar un encabezado {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

La actualización de metadatos de DRM existentes se puede realizar mediante el uso del SDK de Java de Primetime DRM (anteriormente conocido como DRM de acceso a Adobe) para un enfoque programático. Para obtener más información, consulte la [!DNL RegenerateMetadata.java] ejemplo de código en [!DNL /Reference Implmentation/Command Line Tools/samples/] del SDK. El SDK de Java de acceso a Adobe no forma parte de este kit de protección CloudDRM y debe adquirirse directamente desde el Adobe. Póngase en contacto con el contacto profesional del Adobe para obtener más información.
