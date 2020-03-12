---
seo-title: Implementación del servidor Adobe Primetime DRM para flujo protegido
title: Implementación del servidor Adobe Primetime DRM para flujo protegido
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Implementación del servidor Adobe Primetime DRM para flujo protegido{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Para poder implementar Adobe Primetime DRM Server para flujo protegido, debe haber instalado las versiones de Java y Tomcat tal como se indica en el tema Requisitos.

El paquete Primetime DRM Server for Protected Streaming incluye [!DNL flashaccesserver.war]. Si:

* Desea implementar este archivo WAR, debe copiarlo en el directorio de Tomcat [!DNL webapps] .
* Si ya ha implementado el archivo WAR, es posible que deba eliminar el directorio WAR desempaquetado ( [!DNL flashaccessserver] en el directorio [!DNL webapps] de Tomcat).

* Quiere evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] archivo en el directorio [!DNL conf] de Tomcat y configure el `unpackWARs` atributo configurándolo en `false`.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Si ha configurado Tomcat para que incluya [!DNL commons-logging.jar] en la ruta de clases del sistema (no es necesario para Primetime DRM Server para flujo protegido), debe configurar el registro común para utilizar Log4J.

Opcionalmente, el servidor utiliza una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux para un rendimiento óptimo. Puede copiar la biblioteca adecuada para su plataforma desde la [!DNL thirdparty/cryptoj/]*plataforma *a una ubicación especificada por la variable de`PATH`entorno o`LD_LIBRARY_PATH`en Linux.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Sólo debe utilizar la versión de 64 bits si tanto el sistema operativo como el JDK admiten 64 bits. De lo contrario, debe utilizar la versión de 32 bits.

