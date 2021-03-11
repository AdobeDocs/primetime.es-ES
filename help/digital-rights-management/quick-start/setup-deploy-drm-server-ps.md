---
title: Configuración e implementación del servidor para la transmisión protegida
description: Configuración e implementación del servidor para la transmisión protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Configure e implemente el servidor para la transmisión protegida {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configure la carpeta de configuración en el DVD de Primetime DRM:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copie la carpeta `configs` de ejemplo en su `<Tomcat_installation_dir>` y cambie el nombre de la carpeta copiada a `licenseserver`.

   La ruta a la carpeta de configuraciones debe ser `<Tomcat_install_dir>\licenseserver\`.
1. Ejecute `Scrambler.bat` para obtener las contraseñas cifradas para los archivos PFX del servidor de transporte y licencias en el directorio Primetime DRM `<DVD>` `\Adobe Access Server for Protected Streaming\`:

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

1. Copie el archivo `flashaccessserver.war` del CD al directorio `<TomcatInstallDir>\webapps\`.
1. Si Tomcat se está ejecutando, detenga la instancia de Tomcat en ejecución pulsando `<CTRL-C>` en la ventana de comandos (si se inició desde la ventana de comandos). También puede detener el servidor desde la aplicación Servicios de Windows si Tomcat estaba instalado como Servicio de Windows.
1. Para iniciar Tomcat, introduzca el siguiente comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para verificar la configuración, introduzca la siguiente URL en un explorador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
