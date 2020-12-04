---
seo-title: Configuración e implementación del servidor para flujo continuo protegido
title: Configuración e implementación del servidor para flujo continuo protegido
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Configure e implemente el servidor para el flujo protegido {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configure la carpeta de configuración en el DVD de Primetime DRM:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copie la carpeta `configs` de muestra en su `<Tomcat_installation_dir>` y cambie el nombre de la carpeta copiada a `licenseserver`.

   La ruta a la carpeta configs debe ser `<Tomcat_install_dir>\licenseserver\`.
1. Ejecute `Scrambler.bat` para obtener las contraseñas cifradas para los archivos PFX del servidor de transporte y licencia en el directorio Primetime DRM `<DVD>` `\Adobe Access Server for Protected Streaming\`:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copie los archivos PFX en el directorio `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\`.
1. Edite la configuración del inquilino correspondiente en `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, con la siguiente configuración:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Ejecute la utilidad `Validator.bat` para verificar que la configuración es válida:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copie el archivo `flashaccessserver.war` del CD en el directorio `<TomcatInstallDir>\webapps\`.
1. Si Tomcat se está ejecutando, detenga la instancia de Tomcat ejecutándose pulsando `<CTRL-C>` en la ventana de comandos (si se inició desde la ventana de comandos). También puede detener el servidor desde la aplicación Servicios de Windows si Tomcat se instaló como un servicio de Windows.
1. Para inicio Tomcat, introduzca el siguiente comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para verificar la configuración, introduzca la siguiente URL en un explorador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
