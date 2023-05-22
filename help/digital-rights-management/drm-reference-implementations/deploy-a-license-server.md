---
title: Implementación del servidor de licencias
description: Implementación del servidor de licencias
copied-description: true
exl-id: 1439a5b2-eccb-41b7-a4d3-0673e727fb13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Implementación del servidor de licencias{#deploy-the-license-server}

1. Copie los archivos WAR de implementación de referencia en `webapps` en su servidor Tomcat.

   Para utilizar el servidor de licencias de implementación de referencia tal cual, simplemente copie el archivo WAR del servidor de licencias ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) a la `webapps` en su servidor Tomcat.

   Si va a personalizar el servidor de licencias de implementación de referencia, copie los archivos WAR de servidor creados desde `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` a la `webapps` directorio.

   >[!NOTE]
   >
   >Si ha implementado anteriormente archivos WAR del servidor de licencias, es posible que tenga que eliminar los directorios WAR desempaquetados en el [!DNL webapps] en el servidor Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >No implementar [!DNL edsws.war] a menos que necesite compatibilidad con versiones anteriores del contenido de Flash Media Rights Management (FMRMS) v1.5. (Se trata de un requisito muy poco frecuente).
   >
   >Si prefiere evitar que Tomcat descomprima archivos WAR, edite `server.xml` en el `conf` directorio y conjunto `unpackWARs` hasta `false`.

1. Copie todo el contenido del `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` en su [!DNL tomcat] directorio.

   El [!DNL resources] El directorio incluye:

   * [!DNL flashaccesstools.properties] - El archivo de propiedades del servidor de licencias.
   * [!DNL log4j.xml] - Configuración del registro del servidor de licencias
   * [!DNL *.pol] - Archivos de política DRM de muestra.

   Además, también puede copiar los archivos de certificación de Adobe en esta ubicación.

1. Modificación de la configuración del servidor de licencias en [!DNL flashaccesstools.properties] para reflejar la configuración del servidor.

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

1. Edite el `catalina.properties` en su Tomcat `conf` directorio; agregue la ubicación de su [!DNL resources] (o la ubicación alternativa donde haya almacenado el archivo de propiedades y otros archivos de recursos) en el `shared.loader` propiedad.

   Por ejemplo, si tiene `flashaccess-refimpl.properties` ubicado en [!DNL [Tomcat home]\recursos\]:

   ```
   shared.loader=..\resources
   ```

   Estos lugares `flashaccess-refimpl.properties` en la ruta de clase.
1. Asegúrese de que los demás archivos de recursos ( [!DNL log4j.xml], archivos de directivas, certificaciones) se encuentran en la variable [!DNL resources] o están en la ruta de clase y su ubicación especificada en [!DNL flashaccess-refimpl.properties].

   Es probable que desee ejecutar inicialmente `log4j` en modo de depuración. Entrada [!DNL log4j.xml], configurado `debug` a true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Del Tomcat [!DNL bin] directorio, inicie el servidor.

   En Linux:

   ```
   catalina.sh start
   ```

   En Windows:

   ```
   catalina.bat start
   ```
