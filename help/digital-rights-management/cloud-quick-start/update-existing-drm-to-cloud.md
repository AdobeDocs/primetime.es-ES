---
title: Actualizar el contenido DRM existente para utilizar Cloud DRM (opcional)
description: Actualizar el contenido DRM existente para utilizar Cloud DRM (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Actualizar el contenido DRM existente para utilizar Cloud DRM (opcional) {#update-existing-drm-content-to-use-cloud-drm-optional}

Si tiene una biblioteca de contenido existente protegida por el DRM de Primetime, es posible &quot;volver a encabezado&quot; el contenido existente para utilizar el servicio DRM de Primetime Cloud, en lugar de tener que volver a empaquetar/encriptar los archivos de origen originales. El nuevo encabezado del contenido simplemente actualiza los metadatos DRM del contenido en el manifiesto HLS. No realiza ninguna desencriptación/reencriptación del recurso original. Esta puede ser una opción útil si el contenido de origen original no está disponible o si existe preocupación por la cantidad de recursos necesarios para volver a empaquetar una biblioteca grande.

Es posible utilizar el SDK Java de DRM de Primetime para actualizar los metadatos mediante programación. Además, la herramienta de línea de comandos [!DNL OfflinePackager.jar] incluida con este Kit de protección también puede realizar esta tarea mediante la opción `-drm_refresh`.

## Detalles del nuevo encabezado {#section_3F3980D8E775450588C64E02A8448189}

El nuevo encabezado debe actualizar los siguientes campos para utilizar CloudDRM:

* URL del servidor de licencias (A [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificado de servidor de licencias (al certificado de servidor de licencias CloudDRM)
* Certificado de transporte (al certificado de transporte CloudDRM)
* Credencial de Packager (a la credencial de packager que ha activado para su uso con CloudDRM)

## Búsqueda de los metadatos DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

El contenido que utiliza tecnología HTTP (como HDS o HLS) utiliza un manifiesto que hace referencia a los metadatos DRM de acceso al Adobe. En HDS, la etiqueta `<drmmeta>` hace referencia a los metadatos y, en HLS, la etiqueta `#EXT-X-FAXS-CM` hace referencia a ellos. En cualquier escenario, los metadatos se pueden incluir en línea en el manifiesto como blob codificado base-64 o se pueden hacer referencia externamente como archivo binario. Si los metadatos están incrustados/en línea en el manifiesto, es posible que tenga que descodificarlos primero en base64 (decodificarlos en datos binarios) antes de usar esos datos para crear instancias de metadatos DRM.

## Uso del archivo OfflinePacakger.jar incluido {#section_37C2091856E44AA380D742C72B4DD1A7}

Proporcione el `-drm_refresh option` a la línea de comandos. Se creará un nuevo archivo de manifiesto con metadatos DRM actualizados, mientras que el contenido no se volverá a cifrar.

## Uso del SDK Java de DRM de Primetime para el reencabezado {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

La actualización de un DRM existente se puede realizar utilizando el SDK de Java de Primetime DRM (anteriormente conocido como DRM de acceso a Adobe) para un enfoque programático. Para obtener más información, consulte el ejemplo de código [!DNL RegenerateMetadata.java] en el paquete [!DNL /Reference Implmentation/Command Line Tools/samples/] del SDK. El SDK de Java para acceso a Adobe no forma parte de este Kit de protección CloudDRM y debe adquirirse directamente desde el Adobe. Póngase en contacto con su contacto comercial de Adobe para obtener más información.