---
title: Implementación del servidor Adobe Primetime DRM para transmisión protegida
description: Implementación del servidor Adobe Primetime DRM para transmisión protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Implementación del servidor Adobe Primetime DRM para transmisión protegida{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Para poder implementar el servidor Adobe Primetime DRM para la transmisión protegida, debe haber instalado las versiones de Java y Tomcat tal como se indica en el tema Requisitos .

El paquete Primetime DRM Server para transmisión protegida incluye [!DNL flashaccesserver.war]. Si:

* Si desea implementar este archivo WAR, debe copiarlo en el directorio [!DNL webapps] de Tomcat.
* Ya ha implementado anteriormente el archivo WAR, es posible que tenga que eliminar el directorio WAR desempaquetado ( [!DNL flashaccessserver] en el directorio [!DNL webapps] de Tomcat).

* Desea evitar que Tomcat desempaquete archivos WAR, edite el archivo [!DNL server.xml] en el directorio [!DNL conf] de Tomcat y configure el atributo `unpackWARs` configurándolo en `false`.

>[!NOTE]
>
>Si ha configurado Tomcat para incluir [!DNL commons-logging.jar] en la ruta de clase del sistema (no necesaria para el servidor de Primetime DRM para transmisión protegida), debe configurar el registro de recursos comunes para utilizar Log4J.

El servidor opcionalmente utiliza una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux para obtener un rendimiento óptimo. Puede copiar la biblioteca adecuada para su plataforma de [!DNL thirdparty/cryptoj/]*platform* a una ubicación especificada por la variable de entorno `PATH` o `LD_LIBRARY_PATH` en Linux.

>[!NOTE]
>
>Solo debe utilizar la versión de 64 bits si tanto el sistema operativo como el JDK admiten 64 bits. De lo contrario, debe utilizar la versión de 32 bits.

