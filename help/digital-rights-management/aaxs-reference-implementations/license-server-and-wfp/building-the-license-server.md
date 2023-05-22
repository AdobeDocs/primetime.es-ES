---
title: Creación del servidor de licencias
description: Creación del servidor de licencias
copied-description: true
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Creación del servidor de licencias {#building-the-license-server}

El servidor de licencias de implementación de referencia incluye archivos WAR para implementar el servidor de licencias. También incluye todo el código fuente del servidor de licencias y una secuencia de comandos de compilación Ant (Referencia Implementation\Server\refimpl\build-refimpl.xml) para que pueda realizar fácilmente cambios en el código.

>[!NOTE]
>
>Este paso solo es necesario si desea modificar el código fuente. Para fines de evaluación, puede omitir este paso y utilizar los archivos WAR tal como se enviaron.

Antes de ejecutar el script Ant, modifique el script para especificar las ubicaciones del SDK de acceso a Adobe, Tomcat, MySQL y Log4J. Abra build-refimpl.xml en un editor de texto y edite los valores de las propiedades `sdkdir, tomcatdir, mysqldir, and log4jdir`. Para compilar el código fuente y crear los archivos WAR para la implementación de referencia, ejecute la secuencia de comandos utilizando `ant -f build-refimpl.xml all` en el directorio que contiene el script Ant. Una vez finalizado el script, se muestra un [!DNL refimpl-build/wars] se creará el directorio que contiene los archivos WAR del servidor.
