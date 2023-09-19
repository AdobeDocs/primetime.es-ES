---
description: Para actualizar un servidor que ejecute Adobe Access Server for Protected Streaming, reemplace el archivo flashaccessserver.war implementado en el servidor de aplicaciones por el archivo incluido con el último acceso de Adobe. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con el último acceso de Adobe.
title: Ejecución de Adobe Access Server para flujo protegido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Ejecución de Adobe Access Server para flujo protegido{#running-the-adobe-access-server-for-protected-streaming}

Para actualizar un servidor que ejecute Adobe Access Server for Protected Streaming, reemplace el archivo flashaccessserver.war implementado en el servidor de aplicaciones por el archivo incluido con el último acceso de Adobe. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con el último acceso de Adobe.

Antes de ejecutar Adobe Access Server para flujo protegido, Adobe recomienda comprobar que los archivos de configuración son válidos mediante las utilidades proporcionadas con el servidor de licencias. Para obtener más información, consulte &quot;[Validador de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para iniciar Tomcat y el servidor de licencias, ejecute &quot;catalina.bat start&quot; o &quot;catalina.sh start&quot; desde el directorio bin de Tomcat.

Una vez iniciado el servidor, compruebe que está configurado correctamente abriendo *https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1* en una ventana del explorador. Si la configuración del inquilino se cargó correctamente, se muestra un mensaje de confirmación.
