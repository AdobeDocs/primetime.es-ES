---
seo-title: Configuración e implementación del servidor para flujo continuo protegido
title: Configuración e implementación del servidor para flujo continuo protegido
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Configuración e implementación del servidor para flujo continuo protegido {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configure la carpeta de configuración en el DVD de Primetime DRM:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copie la carpeta de muestra en la `configs` carpeta `<Tomcat_installation_dir>` y cambie el nombre de la carpeta copiada a `licenseserver`.

   La ruta a la carpeta de configuraciones ahora debe ser `<Tomcat_install_dir>\licenseserver\`.
1. Ejecute `Scrambler.bat` para obtener las contraseñas cifradas de los archivos PFX del servidor de transporte y licencia en el directorio Primetime DRM `<DVD>``\Adobe Access Server for Protected Streaming\` :

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

1. Ejecute la `Validator.bat` utilidad para comprobar que la configuración es válida:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copie el `flashaccessserver.war` archivo del CD en el `<TomcatInstallDir>\webapps\` directorio.
1. Si Tomcat se está ejecutando, detenga la instancia de Tomcat ejecutándose pulsando `<CTRL-C>` en la ventana de comandos (si se ha iniciado desde la ventana de comandos). También puede detener el servidor desde la aplicación Servicios de Windows si Tomcat se instaló como un servicio de Windows.
1. Para iniciar Tomcat, introduzca el siguiente comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para verificar la configuración, introduzca la siguiente URL en un explorador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
