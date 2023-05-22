---
title: Configurar e implementar el servidor para flujo protegido
description: Configurar e implementar el servidor para flujo protegido
copied-description: true
exl-id: de1488e6-ccee-49e6-999e-6c6762dd55be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Configurar e implementar el servidor para flujo protegido {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configure la carpeta de configuración en el DVD DRM de Primetime:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copiar el ejemplo `configs` carpeta a su `<Tomcat_installation_dir>` y cambie el nombre de la carpeta copiada a `licenseserver`.

   La ruta a la carpeta de configuraciones debe ser ahora `<Tomcat_install_dir>\licenseserver\`.
1. Ejecutar `Scrambler.bat` para obtener las contraseñas cifradas para los archivos PFX del servidor de transporte y licencias en el DRM de Primetime `<DVD>` `\Adobe Access Server for Protected Streaming\` directorio:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copie los archivos PFX en el `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` directorio.
1. Edite la configuración del inquilino correspondiente en `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, con la siguiente configuración:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Ejecute el `Validator.bat` Utilidad para comprobar que la configuración es válida:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copie el `flashaccessserver.war` desde el CD al `<TomcatInstallDir>\webapps\` directorio.
1. Si Tomcat está en ejecución, detenga la instancia de Tomcat en ejecución pulsando `<CTRL-C>` en la ventana de comandos (si se inició desde la ventana de comandos). También puede detener el servidor desde la aplicación Servicios de Windows si Tomcat se ha instalado como servicio de Windows.
1. Para iniciar Tomcat, introduzca el siguiente comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para comprobar la configuración, introduzca la siguiente URL en un explorador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
