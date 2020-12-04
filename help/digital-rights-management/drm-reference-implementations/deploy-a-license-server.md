---
description: 'null'
seo-description: 'null'
seo-title: Implementar el servidor de licencias
title: Implementar el servidor de licencias
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Implementar el servidor de licencias{#deploy-the-license-server}

1. Copie los archivos de guerra de implementación de referencia en el directorio `webapps` de su servidor Tomcat.

   Para utilizar el servidor de licencias de implementación de referencia tal cual, simplemente puede copiar el archivo WAR del servidor de licencias ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) en el directorio `webapps` de su servidor Tomcat.

   Si está personalizando el servidor de licencias de implementación de referencia, copie los archivos de guerra del servidor creados desde `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` al directorio `webapps`.

   >[!NOTE]
   >
   >Si implementó anteriormente archivos WAR del servidor de licencias, es posible que tenga que eliminar los directorios WAR sin empaquetar en el directorio [!DNL webapps] del servidor Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >No implemente [!DNL edsws.war] a menos que necesite compatibilidad con versiones anteriores con contenido de Flash Media Rights Management (FMRMS) v1.5. (Este es un requisito muy raro).
   >
   >Si prefiere evitar que Tomcat descomprima archivos WAR, edite `server.xml` en el directorio `conf` y defina `unpackWARs` en `false`.

1. Copie todo el contenido del directorio `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` en su directorio [!DNL tomcat].

   El directorio [!DNL resources] incluye:

   * [!DNL flashaccesstools.properties] - El archivo de propiedades del servidor de licencias.
   * [!DNL log4j.xml] - Configuración de registro del servidor de licencias
   * [!DNL *.pol] - Archivos de política DRM de muestra.

   Además, también puede elegir copiar los archivos de certificación de Adobe en esta ubicación.

1. Modifique la configuración del servidor de licencias en [!DNL flashaccesstools.properties] para reflejar la configuración del servidor.

   Como mínimo, defina los valores para las siguientes propiedades:

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

1. Edite el archivo `catalina.properties` en el directorio Tomcat `conf`; agregue la ubicación del directorio [!DNL resources] (o la ubicación alternativa donde ha almacenado el archivo de propiedades y otros archivos de recursos) a la propiedad `shared.loader`.

   Por ejemplo, si tiene `flashaccess-refimpl.properties` ubicado en [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Esto coloca `flashaccess-refimpl.properties` en la ruta de clases.
1. Asegúrese de que los demás archivos de recursos ( [!DNL log4j.xml], archivos de políticas, certificaciones) se encuentran en el directorio [!DNL resources] o bien en la ruta de clases y en su ubicación especificada en [!DNL flashaccess-refimpl.properties].

   Es probable que desee ejecutar `log4j` inicialmente en modo de depuración. En [!DNL log4j.xml], establezca `debug` en true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Desde el directorio Tomcat [!DNL bin], inicio el servidor.

   En Linux:

   ```
   catalina.sh start
   ```

   En Windows:

   ```
   catalina.bat start
   ```
