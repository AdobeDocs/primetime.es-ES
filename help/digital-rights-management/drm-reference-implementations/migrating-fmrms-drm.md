---
description: Para seguir emitiendo licencias para contenido que se haya empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de directivas de licencias y DRM del servidor ES de LiveCycle al nuevo servidor del cliente basado en el SDK de DRM de Adobe Primetime.
title: Migrar de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Migrar de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Para seguir emitiendo licencias para contenido que se haya empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de directivas de licencias y DRM del servidor ES de LiveCycle al nuevo servidor del cliente basado en el SDK de DRM de Adobe Primetime.

Para migrar, complete las siguientes tareas:

1. Información de licencia de importación:

   1. Para importar información de licencia de LiveCycle ES a su servidor basado en DRM de Primetime, consulte los scripts de base de datos de ejemplo en la [!DNL Reference Implementation\Server\migration\db] carpeta.
   1. Ejecute los scripts de ejemplo para exportar los datos relevantes de una base de datos MySQL, Oracle o SQL Server a un formato de archivo CSV.
   1. Después de exportar los datos desde LiveCycle ES, impórtelos a la base de datos.

      La información de licencia exportada incluye lo siguiente:

      * ID de licencia
      * ID de contenido que se asigna en el momento del empaquetado
      * El ID de la política de DRM que se está aplicando.
      * La hora a la que se empaquetó el contenido
      * La clave de cifrado de contenido

      Esta información es necesaria para poder convertir los metadatos de contenido 1.x al formato de metadatos DRM de Primetime. En la implementación de referencia, estos datos se almacenan en la tabla de la base de datos de licencias y los utiliza `RefImplMetadataConvReqHandler`. Para obtener más información, consulte `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler`.


1. Convertir directivas de FMRMS al formato DRM de Primetime:

   1. Antes de poder aplicar las políticas de DRM para convertir metadatos y emitir licencias para contenido de la versión 1.0 o la versión 1.5, convierta las políticas de DRM existentes al formato DRM de Primetime.

      El `Reference Implementation\Server\migration` Esta carpeta incluye un código de ejemplo para crear una política de DRM de Primetime basada en políticas de DRM antiguas. Para migrar de FMRMS 1.0 a Primetime DRM , consulte la `V1_0PolicyConverter.java` muestra.
   1. Compile el código de ejemplo ejecutando `ant-f build-migration.xml build-1.0-converter` , que busca las bibliotecas 1.0 y Primetime DRM en la [!DNL libs/1.0] y [!DNL libs/flashaccess] directorios.

   1. Edite el [!DNL converter.properties] para que apunte a su servidor ES de LiveCycle.
   1. Ejecutar `ant -f build-migration.xml migrate-all-1.0-policies` para convertir todas las directivas DRM de FMRMS 1.0 al formato DRM de Primetime.

      Para migrar de FMRMS 1.5 a Primetime DRM , consulte la `V1_5PolicyConverter.java` muestra.

   1. Compile el código de ejemplo ejecutando `ant-f build-migration.xml build-1.5-converter` , que espera que las bibliotecas 1.5 y 3.0 estén en la [!DNL libs/1.5] y [!DNL libs/flashaccess] directorios.

   1. Edite el [!DNL converter.properties] para que apunte a su servidor ES de LiveCycle.
   1. Ejecutar `ant -f build-migration.xml migrate-all-1.5-policies` para convertir todas las directivas DRM de FMRMS 1.5 al formato DRM de Primetime.

      Las directivas DRM convertidas se guardan como un conjunto de ficheros. El `DRM PolicyConverter` genera un archivo con formato CSV que incluye la asignación de los ID de política de DRM antiguos a los nuevos ID de política de DRM. Puede importar este archivo en la [!DNL PolicyConversion] en la base de datos de implementación de referencia, donde la utiliza `RefImplMetadataConvReqHandler`.

1. Compatibilidad de las solicitudes de compatibilidad de 1.x con `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler` propiedades:

   1. Una vez migrados los datos relevantes a un servidor basado en DRM de Primetime, implemente la compatibilidad con las solicitudes de compatibilidad con 1.x.

      Para ver ejemplos sobre cómo procesar estos tipos de solicitudes, consulte `RefImplUpgradeV1ClientHandler` y `RefImplMetadataConvReqHandler` en la implementación de referencia.
