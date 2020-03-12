---
description: Para actualizar un servidor que ejecute Adobe Access Server para flujo protegido, sustituya el archivo flashaccesserver.war implementado en el servidor de aplicaciones por el archivo incluido con la última versión de Adobe Access. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el archivo flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con la última versión de Adobe Access.
seo-description: Para actualizar un servidor que ejecute Adobe Access Server para flujo protegido, sustituya el archivo flashaccesserver.war implementado en el servidor de aplicaciones por el archivo incluido con la última versión de Adobe Access. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el archivo flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con la última versión de Adobe Access.
seo-title: Ejecución del servidor de Adobe Access para flujo continuo protegido
title: Ejecución del servidor de Adobe Access para flujo continuo protegido
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Ejecución del servidor de Adobe Access para flujo continuo protegido{#running-the-adobe-access-server-for-protected-streaming}

Para actualizar un servidor que ejecute Adobe Access Server para flujo protegido, sustituya el archivo flashaccesserver.war implementado en el servidor de aplicaciones por el archivo incluido con la última versión de Adobe Access. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el archivo flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con la última versión de Adobe Access.

Antes de ejecutar Adobe Access Server for Protected Streaming, Adobe recomienda comprobar que los archivos de configuración son válidos mediante las utilidades proporcionadas con el servidor de licencias. Para obtener más información, consulte &quot;Validador[de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para iniciar Tomcat y el servidor de licencias, ejecute &quot;catalina.bat start&quot; o &quot;catalina.sh start&quot; desde el directorio bin de Tomcat.

Una vez iniciado el servidor, compruebe que esté configurado correctamente abriendo *https:// license-server-host:port/flashaccesserver/inquilino-name/flashaccess/license/v1* en una ventana del explorador. Si la configuración del inquilino se ha cargado correctamente, se muestra un mensaje de confirmación.
