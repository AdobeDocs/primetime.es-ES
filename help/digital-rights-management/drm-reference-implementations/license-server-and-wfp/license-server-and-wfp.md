---
description: El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias completamente funcional que utilice todas las funciones del SDK de Java de Adobe Primetime DRM.
title: Servidor de licencias
exl-id: a928b7ac-9191-4b8c-b038-eb92a09286fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Servidor de licencias {#license-server}

El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias completamente funcional que utilice todas las funciones del SDK de Java de Adobe Primetime DRM.

En esta implementación, los usuarios se autentican en función de las entradas de usuario de una base de datos. El servidor incluye lógica empresarial de demostración para la emisión de licencias y proporciona compatibilidad con Flash Media Rights Management Server 1.0 y 1.5.

## Requisitos del servidor de licencias {#license-server-requirements}

Requisitos del servidor de licencias:

* Instalación de Tomcat 6.0 o posterior
* Instale una base de datos, p. ej., MySQL (disponible en el DVD, en [!DNL Third Party\MySQL])
* Asegúrese de que tiene instalado Java 1.6 o posterior
* Para ejecutar los scripts de compilación de ejemplo, asegúrese de que dispone de Ant 1.8 o posterior

Después de instalar Tomcat y MySQL, póngase en contacto con el Adobe para obtener el conjunto de credenciales de DRM necesarias.

## Generar el servidor de licencias {#build-the-license-server}

>[!NOTE]
>
>La creación del servidor de licencias sólo es necesaria si desea modificar el código fuente. Para fines de evaluación, simplemente puede utilizar los archivos WAR tal como se enviaron.

El servidor de licencias de implementación de referencia incluye todo el código fuente del servidor de licencias ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), junto con una secuencia de comandos de Ant build ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) con el que puede personalizar el servidor de licencias para adaptarlo a sus necesidades comerciales.

1. Modifique el script de generación Ant para especificar las ubicaciones del SDK de DRM de Primetime, Tomcat, MySQL y Log4J.

   Abra el [!DNL build-refimpl.xml] en un editor de texto y establezca estos valores de propiedad:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Ejecute el script de generación Ant con `all` , en el directorio donde se encuentra el script de generación Ant.

   ```
   ant -f build-refimpl.xml all
   ```

   El script de generación Ant crea un [!DNL refimpl-build/wars] que incluye los archivos WAR del servidor.
