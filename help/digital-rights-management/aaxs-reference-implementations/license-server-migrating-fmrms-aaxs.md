---
title: Migración de FMRMS 1.0 o 1.5 a Adobe Access 2.0 y versiones posteriores
description: Migración de FMRMS 1.0 o 1.5 a Adobe Access 2.0 y versiones posteriores
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Migración de FMRMS 1.0 o 1.5 a Adobe Access 2.0 y versiones posteriores {#migrating-from-fmrms-or-to-adobe-access-and-above}

Para seguir emitiendo licencias para el contenido empaquetado con Flash Media Rights Management Server (FMRMS) 1.0 o 1.5, los datos de licencias y directivas deben migrarse del servidor ES de LiveCycle al nuevo servidor del cliente basado en el SDK de acceso a Adobe. Los pasos importantes son:

1. Importando información de licencia
1. Convertir directivas de FMRMS al formato de acceso a Adobe
1. Compatibilidad con las solicitudes de compatibilidad 1.x a través de `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler`

Para importar información de licencia de LiveCycle ES en el servidor basado en Acceso a Adobe, consulte los scripts de base de datos de ejemplo que se proporcionan en la [!DNL Reference Implementation\Server\migration\db] carpeta. Se proporcionan secuencias de comandos de ejemplo para exportar los datos relevantes de una base de datos MySQL, Oracle o SQL Server a un formato de archivo CSV. Una vez exportados los datos, se pueden importar en la base de datos que elija. La información de licencia exportada incluye el ID de licencia, un ID de contenido asignado en el momento del empaquetado, el ID de la directiva utilizada, la hora en que se empaquetó el contenido y la clave de cifrado de contenido. Para el acceso desde el Adobe, esta información es necesaria para convertir los metadatos de contenido 1.x al formato de metadatos de acceso desde el Adobe (consulte `FMRMSv1RequestHandler` y `FMRMSv1MetadataHandler`). En la implementación de referencia, estos datos se almacenan en la tabla de la base de datos de licencias y los utiliza `RefImplMetadataConvReqHandler`.

Las directivas existentes deberán convertirse al formato de acceso al Adobe para poder utilizarlas al convertir metadatos y emitir licencias para contenido 1.0 o 1.5. La carpeta Implementación de referencia\Servidor\migración contiene código de ejemplo para crear una directiva de acceso a Adobe basada en directivas antiguas.

Si está migrando de FMRMS 1.0 a Acceso de Adobe, consulte el ejemplo V1_0PolicyConverter.java. Compile el código de ejemplo ejecutando &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (la secuencia de comandos espera que las bibliotecas 1.0 y de Acceso a Adobe estén en [!DNL libs/1.0] y libs/flashaccess respectivamente). Edite el archivo converter.properties para que apunte a su servidor ES de LiveCycle. Entonces ejecute &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; para convertir todas las directivas de FMRMS 1.0 al formato de acceso a Adobe.

Si está migrando de FMRMS 1.5 a Acceso de Adobe, consulte el ejemplo V1_5PolicyConverter.java. Compile el código de ejemplo ejecutando &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (la secuencia de comandos espera que las bibliotecas 1.5 y 3.0 estén en libs/1.5 y libs/flashaccess respectivamente). Edite el archivo converter.properties para que apunte a su servidor ES de LiveCycle. Entonces ejecute &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; para convertir todas las directivas de FMRMS 1.5 al formato de acceso a Adobe.

Las directivas convertidas se escribirán en un conjunto de archivos. Además, PolicyConverter generará un archivo CSV que contiene la asignación de los ID de directiva antiguos a los nuevos ID de directiva. Este archivo se puede importar a la tabla &quot;PolicyConversion&quot; de la base de datos de implementación de referencia y lo utilizará `RefImplMetadataConvReqHandler`.

Una vez que se hayan migrado los datos relevantes al servidor basado en Acceso a Adobe, estará listo para implementar la compatibilidad con las solicitudes de compatibilidad con 1.x. Consulte `RefImplUpgradeV1ClientHandler` y `RefImplMetadataConvReqHandler` en la implementación de referencia para ver ejemplos de cómo procesar este tipo de solicitudes.
