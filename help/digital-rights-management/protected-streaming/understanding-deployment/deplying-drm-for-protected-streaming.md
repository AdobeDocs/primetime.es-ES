---
seo-title: Implementación del servidor DRM de Adobe Primetime para flujo protegido
title: Implementación del servidor DRM de Adobe Primetime para flujo protegido
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Implementación del servidor DRM de Adobe Primetime para flujo protegido{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Para poder implementar el servidor DRM de Adobe Primetime para flujo protegido, debe haber instalado las versiones de Java y Tomcat tal como se indica en el tema Requisitos.

El paquete Primetime DRM Server for Protected Streaming incluye [!DNL flashaccesserver.war]. Si:

* Si desea implementar este archivo WAR, debe copiarlo en el directorio [!DNL webapps] de Tomcat.
* Ya implementó el archivo WAR, es posible que deba eliminar el directorio WAR desempaquetado ( [!DNL flashaccessserver] en el directorio [!DNL webapps] de Tomcat).

* Desea evitar que Tomcat descomprima archivos WAR, edite el archivo [!DNL server.xml] en el directorio [!DNL conf] de Tomcat y configure el atributo `unpackWARs` configurándolo en `false`.

>[!NOTE]
>
>Si ha configurado Tomcat para que incluya [!DNL commons-logging.jar] en la ruta de clases del sistema (no es necesario para Primetime DRM Server para flujo protegido), debe configurar el registro común para utilizar Log4J.

El servidor opcionalmente utiliza una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux para un rendimiento óptimo. Puede copiar la biblioteca adecuada para su plataforma desde [!DNL thirdparty/cryptoj/]*platform* a una ubicación especificada por la variable de entorno `PATH` o `LD_LIBRARY_PATH` en Linux.

>[!NOTE]
>
>Sólo debe utilizar la versión de 64 bits si tanto el sistema operativo como el JDK admiten 64 bits. De lo contrario, debe utilizar la versión de 32 bits.

