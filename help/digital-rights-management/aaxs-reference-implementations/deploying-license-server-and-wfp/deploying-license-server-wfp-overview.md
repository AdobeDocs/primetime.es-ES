---
seo-title: Implementación del servidor de licencias y del empaquetador de carpetas vigilado información general
title: Implementación del servidor de licencias y del empaquetador de carpetas vigilado información general
uuid: 4b71f2f4-f971-4382-ae41-171f7dfdfe21
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Implementación del servidor de licencias y del empaquetador de carpetas vigilado información general {#deploying-the-license-server-and-watched-folder-packager-overview}

Copie los archivos WAR del servidor de licencias en el directorio [!DNL webapps] de Tomcat. Si ya ha implementado el archivo WAR, es posible que deba eliminar manualmente los directorios WAR desempaquetados ( [!DNL flashaccess], [!DNL edcws], y [!DNL flashaccess-packager] en el [!DNL webapps] directorio de Tomcat). Para evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] archivo en el directorio conf de Tomcat y establezca el `unpackWARs` atributo en `false`.

El archivo de propiedades ( [!DNL flashaccess-refimpl.properties]) debe estar en la ruta de clases para que el servidor cargue las propiedades. Copie este archivo en un directorio y actualice el archivo con los valores correspondientes. Edite el [!DNL catalina.properties] archivo en el directorio [!DNL conf] de Tomcat y agregue el directorio que contiene [!DNL flashaccess-refimpl.properties] a la `shared.loader` propiedad. El [!DNL log4j.xml] archivo para configurar el registro también debe estar en la ruta de clases (consulte [!DNL resources\log4j.xml] un ejemplo).

El servidor de implementación de referencia utiliza varios archivos de certificado, archivos de política y otros recursos. Todos estos archivos se encuentran en una carpeta de recursos. De forma predeterminada, la carpeta de recursos es [!DNL C:\flashaccess-server-resources]pero esta ubicación se puede modificar en [!DNL flashaccess-refimpl.properties]. Asegúrese de copiar todos los recursos necesarios en esta ubicación antes de iniciar el servidor.

Para iniciar Tomcat y el servidor de licencias, ejecute `catalina.bat start` desde el [!DNL bin] directorio de Tomcat.
