---
description: Para seguir emitiendo licencias para contenido que se ha empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de licencia y de directiva DRM desde el servidor LiveCycle ES al nuevo servidor del cliente basado en el SDK de DRM de Adobe Primetime.
seo-description: Para seguir emitiendo licencias para contenido que se ha empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de licencia y de directiva DRM desde el servidor LiveCycle ES al nuevo servidor del cliente basado en el SDK de DRM de Adobe Primetime.
seo-title: Migración de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior
title: Migración de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Migración de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Para seguir emitiendo licencias para contenido que se ha empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de licencia y de directiva DRM desde el servidor LiveCycle ES al nuevo servidor del cliente basado en el SDK de DRM de Adobe Primetime.

Para migrar, complete las siguientes tareas:

1. Importar información de licencia:

   1. Para importar información de licencia de LiveCycle ES a su servidor basado en DRM de Primetime, consulte las secuencias de comandos de base de datos de ejemplo en la [!DNL Reference Implementation\Server\migration\db] carpeta.
   1. Ejecute las secuencias de comandos de ejemplo para exportar datos relevantes desde una base de datos MySQL, Oracle o SQL Server a un formato de archivo CSV.
   1. Después de exportar los datos desde LiveCycle ES, importe los datos a la base de datos.

      La información de la licencia exportada incluye lo siguiente:

      * Un ID de licencia
      * ID de contenido que se asigna en el momento del empaquetado
      * ID de la directiva DRM que se está aplicando
      * Hora a la que se empaquetó el contenido
      * La clave de cifrado de contenido
      Esta información es necesaria para poder convertir los metadatos de contenido 1.x al formato de metadatos DRM Primetime. En la implementación de referencia, estos datos se almacenan en la tabla de la base de datos de licencias y son utilizados por `RefImplMetadataConvReqHandler`. For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.


1. Conversión de directivas FMRMS al formato DRM Primetime:

   1. Antes de aplicar las políticas de DRM para convertir metadatos y emitir licencias para contenido de la versión 1.0 o la versión 1.5, convierta las directivas de DRM existentes al formato de DRM Primetime.

      La `Reference Implementation\Server\migration` carpeta incluye código de muestra para crear una directiva DRM de Primetime basada en directivas DRM antiguas. Para migrar de FMRMS 1.0 a Primetime DRM, consulte el `V1_0PolicyConverter.java` ejemplo.
   1. Compile el código de muestra ejecutando `ant-f build-migration.xml build-1.0-converter` script, que busca las bibliotecas 1.0 y Primetime DRM en los directorios [!DNL libs/1.0] y [!DNL libs/flashaccess] .

   1. Edite el [!DNL converter.properties] archivo para que señale a su servidor LiveCycle ES.
   1. Ejecute `ant -f build-migration.xml migrate-all-1.0-policies` para convertir todas las directivas DRM de FMRMS 1.0 al formato DRM de Primetime.

      Para migrar de FMRMS 1.5 a Primetime DRM, consulte el `V1_5PolicyConverter.java` ejemplo.

   1. Compile el código de muestra ejecutando `ant-f build-migration.xml build-1.5-converter` script, que espera que las bibliotecas 1.5 y 3.0 estén en los directorios [!DNL libs/1.5] y [!DNL libs/flashaccess] .

   1. Edite el [!DNL converter.properties] archivo para que señale a su servidor LiveCycle ES.
   1. Ejecute `ant -f build-migration.xml migrate-all-1.5-policies` para convertir todas las directivas DRM de FMRMS 1.5 al formato DRM de Primetime.

      Las directivas de DRM convertidas se guardan como un conjunto de archivos. El `DRM PolicyConverter` genera un archivo con formato CSV que incluye la asignación de los ID de directiva de DRM antiguos a los ID de directiva de DRM nuevos. Puede importar este archivo a la [!DNL PolicyConversion] tabla de la base de datos de implementación de referencia, donde `RefImplMetadataConvReqHandler`.

1. Admite las solicitudes de compatibilidad de 1.x con las propiedades `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler` :

   1. Una vez migrados los datos relevantes a un servidor basado en DRM de Primetime, implemente la compatibilidad con solicitudes de compatibilidad con 1.x.

      Para obtener ejemplos sobre cómo procesar estos tipos de solicitudes, consulte `RefImplUpgradeV1ClientHandler` y `RefImplMetadataConvReqHandler` en la implementación de referencia.

