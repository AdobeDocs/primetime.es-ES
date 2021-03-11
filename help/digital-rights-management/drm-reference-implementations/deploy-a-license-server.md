---
title: Implementar el servidor de licencias
description: Implementar el servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Implementar el servidor de licencias{#deploy-the-license-server}

1. Copie los archivos war de implementación de referencia en el directorio `webapps` de su servidor Tomcat.

   Para utilizar el servidor de licencias de implementación de referencia tal cual, simplemente puede copiar el archivo WAR del servidor de licencias ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) en el directorio `webapps` de su servidor Tomcat.

   Si está personalizando el servidor de licencias de implementación de referencia, copie los archivos de guerra del servidor que ha generado desde `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` al directorio `webapps`.

   >[!NOTE]
   >
   >Si ha implementado anteriormente archivos WAR del servidor de licencias, es posible que tenga que eliminar los directorios WAR desempaquetados en el directorio [!DNL webapps] del servidor Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >No implemente [!DNL edsws.war] a menos que requiera compatibilidad con versiones anteriores con contenido de Flash Media Rights Management (FMRMS) v1.5. (Este es un requisito muy raro).
   >
   >Si prefiere evitar que Tomcat desempaquete archivos WAR, edite `server.xml` en el directorio `conf` y establezca `unpackWARs` en `false`.

1. Copie todo el contenido del directorio `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` en su directorio [!DNL tomcat].

   El directorio [!DNL resources] incluye:

   * [!DNL flashaccesstools.properties] - El archivo de propiedades del servidor de licencias.
   * [!DNL log4j.xml] - Configuración del registro del servidor de licencias
   * [!DNL *.pol] - Archivos de política DRM de muestra.

   Además, también puede elegir copiar los archivos de certificación de Adobe en esta ubicación.

1. Modifique la configuración del servidor de licencias en [!DNL flashaccesstools.properties] para que refleje la configuración del servidor.

   Como mínimo, establezca valores para las siguientes propiedades:

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. Edite el archivo `catalina.properties` en el directorio Tomcat `conf`; agregue la ubicación del directorio [!DNL resources] (o la ubicación alternativa donde haya almacenado el archivo de propiedades y otros archivos de recursos) a la propiedad `shared.loader` .

   Por ejemplo, si tiene `flashaccess-refimpl.properties` ubicado en [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Esto coloca `flashaccess-refimpl.properties` en la ruta de la clase.
1. Asegúrese de que los demás archivos de recursos ( [!DNL log4j.xml], archivos de directivas, certificaciones) se encuentran en el directorio [!DNL resources] o bien están en la ruta de clase y en su ubicación especificada en [!DNL flashaccess-refimpl.properties].

   Es probable que desee ejecutar inicialmente `log4j` en modo de depuración. En [!DNL log4j.xml], establezca `debug` en true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Desde el directorio Tomcat [!DNL bin], inicie su servidor.

   En Linux:

   ```
   catalina.sh start
   ```

   En Windows:

   ```
   catalina.bat start
   ```
