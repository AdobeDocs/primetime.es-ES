---
seo-title: Creación del servidor de licencias
title: Creación del servidor de licencias
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Creación del servidor de licencias {#building-the-license-server}

El servidor de licencias de implementación de referencia incluye archivos WAR para implementar el servidor de licencias. También incluye todo el código fuente del servidor de licencias y una secuencia de comandos de compilación de Ant (Referencia Implementation\Server\refimpl\build-refimpl.xml) para que pueda realizar cambios en el código fácilmente.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Este paso solo es necesario si desea modificar el código fuente. A efectos de evaluación, puede omitir este paso y utilizar los archivos WAR tal como se enviaron.

Antes de ejecutar el script Ant, modifique el script para especificar las ubicaciones del SDK de Adobe Access, Tomcat, MySQL y Log4J. Abra build-refimpl.xml en un editor de texto y edite los valores de las propiedades `sdkdir, tomcatdir, mysqldir, and log4jdir`. Para compilar el código fuente y crear los archivos WAR para la implementación de referencia, ejecute la secuencia de comandos utilizando `ant -f build-refimpl.xml all` el directorio que contiene la secuencia de comandos Ant. Cuando la secuencia de comandos esté completa, se creará un [!DNL refimpl-build/wars] directorio que contenga los archivos WAR del servidor.
