---
title: Migración de FMRMS 1.0 o 1.5 a Adobe Access 2.0 y posterior
description: Migración de FMRMS 1.0 o 1.5 a Adobe Access 2.0 y posterior
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Migración de FMRMS 1.0 o 1.5 a Adobe Access 2.0 y superior {#migrating-from-fmrms-or-to-adobe-access-and-above}

Para seguir emitiendo licencias para contenido empaquetado mediante Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, los datos de licencia y directiva deben migrarse del servidor de LiveCycle ES al nuevo servidor del cliente basado en el SDK de acceso a Adobe. Los pasos importantes son:

1. Importación de información de licencia
1. Conversión de directivas de FMRMS al formato de acceso a Adobe
1. Soporte de las solicitudes de compatibilidad de 1.x a través de `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler`

Para importar información de licencia de LiveCycle ES a su servidor basado en Access de Adobe, consulte los scripts de base de datos de ejemplo que se proporcionan en la carpeta [!DNL Reference Implementation\Server\migration\db]. Se proporcionan secuencias de comandos de ejemplo para exportar los datos relevantes de una base de datos MySQL, Oracle o SQL Server a un formato de archivo CSV. Una vez exportados los datos, estos se pueden importar en la base de datos que elija. La información de licencia exportada incluye el ID de licencia, un ID de contenido asignado en el momento del empaquetado, el ID de la directiva utilizada, la hora en que se empaquetó el contenido y la clave de cifrado de contenido. Para el acceso a Adobe, esta información es necesaria para convertir los metadatos de contenido de 1.x al formato de metadatos de acceso a Adobe (consulte `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler`). En la implementación de referencia, estos datos se almacenan en la tabla de la base de datos de licencias y se utilizan en `RefImplMetadataConvReqHandler`.

Las políticas existentes deberán convertirse al formato de acceso a Adobe para poder usar esas políticas al convertir metadatos y emitir licencias para contenido de 1.0 o 1.5. La Referencia Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies.

Si está migrando de FMRMS 1.0 a Adobe Access, consulte la muestra V1_0PolicyConverter.java . Compile el código de muestra ejecutando &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (el script espera que las bibliotecas 1.0 y Adobe Access estén en [!DNL libs/1.0] y libs/flashaccess respectivamente). Edite el archivo conversion.properties para que apunte a su servidor ES de LiveCycle. A continuación, ejecute &quot;`ant -f build-migration.xml migrate-all-1.0-policies`&quot; para convertir todas las directivas de FMRMS 1.0 al formato de acceso a Adobe.

Si está migrando de FMRMS 1.5 a Acceso a Adobe, consulte la muestra V1_5PolicyConverter.java . Compile el código de muestra ejecutando &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (el script espera que las bibliotecas 1.5 y 3.0 estén en libs/1.5 y libs/flashaccess respectivamente). Edite el archivo conversion.properties para que apunte a su servidor ES de LiveCycle. A continuación, ejecute &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; para convertir todas las directivas de FMRMS 1.5 al formato de acceso a Adobe.

Las políticas convertidas se escribirán en un conjunto de archivos. Además, PolicyConverter generará un archivo CSV que contendrá la asignación de ID de directivas antiguas a ID de directivas nuevos. Este archivo se puede importar en la tabla &quot;PolicyConversion&quot; de la base de datos de implementación de referencia y será utilizado por `RefImplMetadataConvReqHandler`.

Una vez que los datos relevantes se hayan migrado al servidor basado en Adobe Access, estará listo para implementar la compatibilidad con las solicitudes de compatibilidad con 1.x. Consulte `RefImplUpgradeV1ClientHandler` y `RefImplMetadataConvReqHandler` en la implementación de referencia para ver ejemplos sobre cómo procesar estos tipos de solicitudes.
