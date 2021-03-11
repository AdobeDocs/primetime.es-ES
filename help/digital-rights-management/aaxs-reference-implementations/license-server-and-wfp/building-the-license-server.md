---
title: Creación del servidor de licencias
description: Creación del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Creación del servidor de licencias {#building-the-license-server}

El servidor de licencias de implementación de referencia incluye archivos WAR para implementar el servidor de licencias. También incluye todo el código fuente del servidor de licencias y un script de compilación de Ant (consulte Implementation\Server\refimpl\build-refimpl.xml) para que pueda realizar cambios fácilmente en el código.

>[!NOTE]
>
>Este paso solo es necesario si desea modificar el código fuente. Para fines de evaluación, puede omitir este paso y utilizar los archivos WAR tal como se enviaron.

Antes de ejecutar el script Ant, modifique el script para especificar las ubicaciones del SDK de acceso al Adobe, Tomcat, MySQL y Log4J. Abra build-refimpl.xml en un editor de texto y edite los valores de las propiedades `sdkdir, tomcatdir, mysqldir, and log4jdir`. Para compilar el código fuente y crear los archivos WAR para la implementación de referencia, ejecute el script utilizando `ant -f build-refimpl.xml all` en el directorio que contiene el script Ant. Cuando se complete el script, se creará un directorio [!DNL refimpl-build/wars] que contiene los archivos WAR del servidor.
