---
description: Para actualizar un servidor que ejecute Adobe Access Server para la transmisión protegida, reemplace el archivo flashaccesserver.war implementado en su servidor de aplicaciones con el archivo incluido con el acceso de Adobe más reciente. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el flashaccess-tenant.xml de su servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con el acceso al Adobe más reciente.
title: Ejecución de Adobe Access Server para transmisión protegida
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Ejecución de Adobe Access Server para transmisión protegida{#running-the-adobe-access-server-for-protected-streaming}

Para actualizar un servidor que ejecute Adobe Access Server para la transmisión protegida, reemplace el archivo flashaccesserver.war implementado en su servidor de aplicaciones con el archivo incluido con el acceso de Adobe más reciente. Si desea utilizar las nuevas opciones de configuración descritas anteriormente, actualice el flashaccess-tenant.xml de su servidor. También debe actualizar jsafe.dll o libjsafe.so a la versión incluida con el acceso al Adobe más reciente.

Antes de ejecutar Adobe Access Server para la transmisión protegida, Adobe recomienda que compruebe que los archivos de configuración son válidos utilizando las utilidades proporcionadas con el servidor de licencias. Para obtener más información, consulte &quot;[Validador de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para iniciar Tomcat y el servidor de licencias, ejecute &quot;catalina.bat start&quot; o &quot;catalina.sh start&quot; desde el directorio bin de Tomcat.

Una vez iniciado el servidor, compruebe que esté configurado correctamente abriendo *https:// license-server-host:port/flashaccesserver/tenant-name/flashaccess/license/v1* en una ventana del explorador. Si la configuración del inquilino se cargó correctamente, se muestra un mensaje de confirmación.
