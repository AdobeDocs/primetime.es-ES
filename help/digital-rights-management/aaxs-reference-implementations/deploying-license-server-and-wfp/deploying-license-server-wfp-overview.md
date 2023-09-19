---
title: Información general sobre la implementación del servidor de licencias y el empaquetador de carpetas inspeccionadas
description: Información general sobre la implementación del servidor de licencias y el empaquetador de carpetas inspeccionadas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Información general sobre la implementación del servidor de licencias y el empaquetador de carpetas inspeccionadas {#deploying-the-license-server-and-watched-folder-packager-overview}

Copie los archivos WAR del servidor de licencias en el de Tomcat. [!DNL webapps] directorio. Si ha implementado previamente el archivo WAR, es posible que tenga que eliminar manualmente los directorios WAR desempaquetados ( [!DNL flashaccess], [!DNL edcws], y [!DNL flashaccess-packager] en Tomcat&#39;s [!DNL webapps] directorio). Para evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] en el directorio conf de Tomcat y configure el `unpackWARs` atribuir a `false`.

El archivo de propiedades ( [!DNL flashaccess-refimpl.properties]) debe estar en la ruta de clase para que el servidor cargue las propiedades. Copie este archivo en un directorio y actualice el archivo con los valores adecuados. Edite el [!DNL catalina.properties] archivo en Tomcat&#39;s [!DNL conf] y añada el directorio que contiene [!DNL flashaccess-refimpl.properties] a la `shared.loader` propiedad. El [!DNL log4j.xml] el archivo para configurar el registro también debe estar en la ruta de clase (consulte [!DNL resources\log4j.xml] por ejemplo).

El servidor de implementación de referencia utiliza varios archivos de certificado, archivos de directivas y otros recursos. Todos esos archivos se encuentran en una carpeta de recursos. De forma predeterminada, la carpeta de recursos es [!DNL C:\flashaccess-server-resources], pero esta ubicación se puede modificar en [!DNL flashaccess-refimpl.properties]. Asegúrese de copiar todos los recursos necesarios en esta ubicación antes de iniciar el servidor.

Para iniciar Tomcat y el servidor de licencias, ejecute `catalina.bat start` de Tomcat&#39;s [!DNL bin] directorio.
