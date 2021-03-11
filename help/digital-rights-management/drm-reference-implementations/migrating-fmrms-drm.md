---
description: Para seguir emitiendo licencias para contenido que se ha empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de licencia y directiva DRM del servidor de LiveCycle ES al nuevo servidor del cliente que se basa en el SDK de Adobe Primetime DRM.
title: Migración de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Migración de FMRMS 1.0 o 1.5 a Adobe Primetime DRM 2.0 o posterior{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Para seguir emitiendo licencias para contenido que se ha empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, debe migrar los datos de licencia y directiva DRM del servidor de LiveCycle ES al nuevo servidor del cliente que se basa en el SDK de Adobe Primetime DRM.

Para migrar, complete las siguientes tareas:

1. Importar información de licencia:

   1. Para importar información de licencia desde LiveCycle ES a su servidor basado en DRM de Primetime, consulte los scripts de base de datos de ejemplo en la carpeta [!DNL Reference Implementation\Server\migration\db] .
   1. Ejecute las secuencias de comandos de ejemplo para exportar los datos relevantes de una base de datos MySQL, Oracle o SQL Server a un formato de archivo CSV.
   1. Después de exportar los datos desde LiveCycle ES, impórtelos en la base de datos.

      La información de licencia exportada incluye lo siguiente:

      * Un ID de licencia
      * Un ID de contenido que se asigna en el momento del empaquetado
      * El ID de la directiva DRM que se está aplicando
      * La hora a la que se empaquetó el contenido
      * La clave de cifrado de contenido

      Esta información es necesaria para poder convertir los metadatos de contenido 1.x al formato de metadatos DRM de Primetime. En la implementación de referencia, estos datos se almacenan en la tabla de la base de datos de licencias y se utilizan en `RefImplMetadataConvReqHandler`. Para obtener más información, consulte `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler`.


1. Convierta las directivas de FMRMS al formato DRM de Primetime:

   1. Antes de poder aplicar las directivas de DRM para convertir metadatos y emitir licencias para contenido de la versión 1.0 o versión 1.5, convierta las directivas de DRM existentes al formato de DRM de Primetime.

      La carpeta `Reference Implementation\Server\migration` incluye código de muestra para crear una directiva de DRM de Primetime basada en directivas de DRM antiguas. Para migrar de FMRMS 1.0 a Primetime DRM , consulte el ejemplo `V1_0PolicyConverter.java`.
   1. Compile el código de muestra ejecutando el script `ant-f build-migration.xml build-1.0-converter`, que busca las bibliotecas 1.0 y Primetime DRM en los directorios [!DNL libs/1.0] y [!DNL libs/flashaccess].

   1. Edite el archivo [!DNL converter.properties] para que apunte a su servidor ES de LiveCycle.
   1. Ejecute `ant -f build-migration.xml migrate-all-1.0-policies` para convertir todas las directivas DRM de FMRMS 1.0 al formato DRM de Primetime.

      Para migrar de FMRMS 1.5 a Primetime DRM , consulte el ejemplo `V1_5PolicyConverter.java`.

   1. Compile el código de muestra ejecutando el script `ant-f build-migration.xml build-1.5-converter` , que espera que las bibliotecas 1.5 y 3.0 estén en los directorios [!DNL libs/1.5] y [!DNL libs/flashaccess] .

   1. Edite el archivo [!DNL converter.properties] para que apunte a su servidor ES de LiveCycle.
   1. Ejecute `ant -f build-migration.xml migrate-all-1.5-policies` para convertir todas las directivas DRM de FMRMS 1.5 al formato DRM de Primetime.

      Las directivas DRM convertidas se guardan como un conjunto de archivos. El `DRM PolicyConverter` genera un archivo con formato CSV que incluye la asignación de los ID de directivas de DRM antiguos a los nuevos ID de directivas de DRM. Puede importar este archivo a la tabla [!DNL PolicyConversion] de la base de datos de implementación de referencia, donde lo utiliza `RefImplMetadataConvReqHandler`.

1. Admite las solicitudes de compatibilidad de 1.x con las propiedades `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler` :

   1. Una vez migrados los datos relevantes a un servidor basado en DRM de Primetime, implemente la compatibilidad con las solicitudes de compatibilidad con 1.x.

      Para obtener ejemplos sobre cómo procesar estos tipos de solicitudes, consulte `RefImplUpgradeV1ClientHandler` y `RefImplMetadataConvReqHandler` en la implementación de referencia.

