---
seo-title: Actualizar el contenido existente de DRM para utilizar Cloud DRM (opcional)
title: Actualizar el contenido existente de DRM para utilizar Cloud DRM (opcional)
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Actualice el contenido existente de DRM para utilizar Cloud DRM (opcional) {#update-existing-drm-content-to-use-cloud-drm-optional}

Si tiene una biblioteca de contenido existente protegida por Primetime DRM, es posible &quot;volver a colocar el encabezado&quot; del contenido existente para utilizar el servicio de DRM de Primetime Cloud, en lugar de tener que volver a empaquetar/cifrar los archivos de origen originales. Al volver a escribir el encabezado del contenido, simplemente se actualizan los metadatos DRM del contenido del manifiesto HLS. No realiza ninguna descodificación o recodificación del recurso original. Esta opción puede resultar útil si el contenido de origen original no está disponible o si existe preocupación por la cantidad de recursos necesarios para volver a empaquetar una biblioteca grande.

Es posible utilizar el SDK de Java de Primetime DRM para actualizar los metadatos mediante programación. Además, la herramienta de línea de comandos [!DNL OfflinePackager.jar] incluida con este Kit de protección también puede llevar a cabo esta tarea mediante la opción `-drm_refresh`.

## Detalles del nuevo encabezado {#section_3F3980D8E775450588C64E02A8448189}

El cambio de encabezado debe actualizar los campos siguientes para utilizar CloudDRM:

* URL del servidor de licencias (a [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificado de servidor de licencias (al certificado de servidor de licencias CloudDRM)
* Certificado de transporte (al certificado de transporte CloudDRM)
* Credenciales de Packager (para las credenciales de Packager que ha activado para su uso con CloudDRM)

## Búsqueda de metadatos DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

El contenido que utiliza tecnología HTTP (como HDS o HLS) utiliza un manifiesto que hace referencia a los metadatos DRM de acceso a Adobe. En HDS, la etiqueta `<drmmeta>` hace referencia a los metadatos y, en HLS, la etiqueta `#EXT-X-FAXS-CM` hace referencia a ellos. En cualquier escenario, los metadatos se pueden incluir en línea en el manifiesto como un blob codificado en base-64, o se pueden hacer referencia externamente como un archivo binario. Si los metadatos están incrustados/integrados en el manifiesto, es posible que primero tenga que descodificarlos en datos binarios antes de utilizar esos datos para crear instancias de metadatos DRM.

## Uso del archivo OfflinePacakger.jar incluido {#section_37C2091856E44AA380D742C72B4DD1A7}

Proporcione el `-drm_refresh option` a la línea de comandos. Se creará un nuevo archivo de manifiesto con metadatos DRM actualizados, mientras que el contenido no se volverá a cifrar.

## Uso del SDK de Java de DRM Primetime para el reencabezado {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

La actualización de metadatos DRM existentes se puede realizar mediante el uso del SDK de Java de DRM Primetime (anteriormente conocido como DRM de acceso Adobe) para un enfoque programático. Para obtener más información, consulte el ejemplo de código [!DNL RegenerateMetadata.java] en el paquete [!DNL /Reference Implmentation/Command Line Tools/samples/] del SDK. El SDK de Java de Adobe Access no forma parte de este kit de protección CloudDRM y debe adquirirse directamente desde Adobe. Póngase en contacto con el contacto comercial de su Adobe para obtener más información.