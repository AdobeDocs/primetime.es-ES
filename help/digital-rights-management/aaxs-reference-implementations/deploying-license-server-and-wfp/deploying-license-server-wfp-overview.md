---
title: Implementación del servidor de licencias y del paquete de carpetas visto
description: Implementación del servidor de licencias y del paquete de carpetas visto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Implementación del servidor de licencias y del paquete de carpetas visto {#deploying-the-license-server-and-watched-folder-packager-overview}

Copie los archivos WAR del servidor de licencias al directorio [!DNL webapps] de Tomcat. Si ha implementado anteriormente el archivo WAR, es posible que tenga que eliminar manualmente los directorios WAR desempaquetados ( [!DNL flashaccess], [!DNL edcws] y [!DNL flashaccess-packager] en el directorio [!DNL webapps] de Tomcat). Para evitar que Tomcat desempaquete archivos WAR, edite el archivo [!DNL server.xml] en el directorio conf de Tomcat y establezca el atributo `unpackWARs` en `false`.

El archivo de propiedades ( [!DNL flashaccess-refimpl.properties]) debe estar en la ruta de clase para que el servidor cargue las propiedades. Copie este archivo en un directorio y actualice el archivo con los valores adecuados. Edite el archivo [!DNL catalina.properties] en el directorio [!DNL conf] de Tomcat y añada el directorio que contiene [!DNL flashaccess-refimpl.properties] a la propiedad `shared.loader`. El archivo [!DNL log4j.xml] para configurar el registro también debe estar en la ruta de la clase (consulte [!DNL resources\log4j.xml] para ver un ejemplo).

El servidor de implementación de referencia utiliza varios archivos de certificado, archivos de directiva y otros recursos. Todos esos archivos están ubicados en una carpeta de recursos. De forma predeterminada, la carpeta de recursos es [!DNL C:\flashaccess-server-resources], pero esta ubicación se puede modificar en [!DNL flashaccess-refimpl.properties]. Asegúrese de copiar todos los recursos necesarios en esta ubicación antes de iniciar el servidor.

Para iniciar Tomcat y el servidor de licencias, ejecute `catalina.bat start` desde el directorio [!DNL bin] de Tomcat.
