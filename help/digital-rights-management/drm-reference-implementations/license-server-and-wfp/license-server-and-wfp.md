---
description: El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias completamente funcional que utilice todas las funciones del SDK de Java de Adobe Primetime DRM.
seo-description: El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias completamente funcional que utilice todas las funciones del SDK de Java de Adobe Primetime DRM.
seo-title: Servidor de licencias
title: Servidor de licencias
uuid: 39cb0d0f-f3dc-48e9-b6fd-6960a9ade291
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Servidor de licencias {#license-server}

El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias completamente funcional que utilice todas las funciones del SDK de Java de Adobe Primetime DRM.

En esta implementación, los usuarios se autentican según las entradas de usuario en una base de datos. El servidor incluye lógica empresarial de demostración para la emisión de licencias y ofrece compatibilidad con Flash Media Rights Management Server 1.0 y 1.5.

## Requisitos del servidor de licencias {#license-server-requirements}

Requisitos del servidor de licencias:

* Instalación de Tomcat 6.0 o posterior
* Instale una base de datos, por ejemplo, MySQL (disponible en el DVD, en [!DNL Third Party\MySQL])
* Asegúrese de tener instalado Java 1.6 o posterior
* Para ejecutar secuencias de comandos de compilación de ejemplo, asegúrese de que dispone de Ant 1.8 o posterior

Después de instalar Tomcat y MySQL, póngase en contacto con Adobe para obtener el conjunto de credenciales de DRM necesarias.

## Genere el servidor de licencias {#build-the-license-server}

>[!NOTE]
>
>La creación del servidor de licencias solo es necesaria si desea modificar el código fuente. Para fines de evaluación, puede simplemente utilizar los archivos WAR tal como se enviaron.

El servidor de licencias de implementación de referencia incluye todo el código fuente del servidor de licencias ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), junto con un script de compilación de Ant ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) con el que puede personalizar el servidor de licencias para adaptarlo a sus necesidades comerciales.

1. Modifique la secuencia de comandos de compilación de Ant para especificar las ubicaciones del SDK de DRM de Primetime, Tomcat, MySQL y Log4J.

   Abra el archivo [!DNL build-refimpl.xml] en un editor de texto y establezca estos valores de propiedad:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Ejecute la secuencia de comandos de compilación de Ant con la propiedad `all`, en el directorio donde se encuentra la secuencia de comandos de compilación de Ant.

   ```
   ant -f build-refimpl.xml all
   ```

   La secuencia de comandos de compilación de Ant crea un directorio [!DNL refimpl-build/wars] que incluye los archivos WAR del servidor.
