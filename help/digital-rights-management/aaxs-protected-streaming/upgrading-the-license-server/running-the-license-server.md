---
description: Para actualizar un servidor que ejecute Adobe Access Server para flujo protegido, reemplace el archivo flashaccesserver.war implementado en el servidor de aplicaciones por el archivo incluido con el acceso de Adobe más reciente. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el archivo flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con la última versión de Adobe Access.
seo-description: Para actualizar un servidor que ejecute Adobe Access Server para flujo protegido, reemplace el archivo flashaccesserver.war implementado en el servidor de aplicaciones por el archivo incluido con el acceso de Adobe más reciente. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el archivo flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con la última versión de Adobe Access.
seo-title: Ejecución del Adobe Access Server para flujo continuo protegido
title: Ejecución del Adobe Access Server para flujo continuo protegido
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Ejecución del Adobe Access Server para flujo protegido{#running-the-adobe-access-server-for-protected-streaming}

Para actualizar un servidor que ejecute Adobe Access Server para flujo protegido, reemplace el archivo flashaccesserver.war implementado en el servidor de aplicaciones por el archivo incluido con el acceso de Adobe más reciente. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el archivo flashaccess-tenant.xml del servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con la última versión de Adobe Access.

Antes de ejecutar Adobe Access Server para flujo continuo protegido, Adobe recomienda comprobar que los archivos de configuración son válidos mediante las utilidades proporcionadas con el servidor de licencias. Para obtener más información, consulte &quot;[Validador de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para inicio Tomcat y el servidor de licencias, ejecute &quot;inicio catalina.bat&quot; o &quot;inicio catalina.sh&quot; desde el directorio bin de Tomcat.

Una vez que el servidor se haya iniciado, verifique que esté configurado correctamente abriendo *https:// license-server-host:port/flashaccesserver/tenant-name/flashaccess/license/v1* en una ventana del explorador. Si la configuración del inquilino se ha cargado correctamente, se muestra un mensaje de confirmación.
