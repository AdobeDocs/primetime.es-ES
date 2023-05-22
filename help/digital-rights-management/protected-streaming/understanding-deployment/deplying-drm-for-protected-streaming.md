---
title: Implementación del servidor DRM de Adobe Primetime para el streaming protegido
description: Implementación del servidor DRM de Adobe Primetime para el streaming protegido
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Implementación del servidor DRM de Adobe Primetime para el streaming protegido{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Antes de poder implementar el servidor DRM de Adobe Primetime para flujo protegido, debe tener instaladas las versiones de Java y Tomcat que se indican en el tema Requisitos.

El paquete Servidor DRM de Primetime para flujo protegido incluye [!DNL flashaccesserver.war]. Si:

* Si desea implementar este archivo WAR, debe copiarlo en el de Tomcat [!DNL webapps] directorio.
* Si ya ha implementado el archivo WAR, es posible que tenga que eliminar el directorio WAR desempaquetado ( [!DNL flashaccessserver] en Tomcat&#39;s [!DNL webapps] directorio).

* Si desea evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] archivo en Tomcat&#39;s [!DNL conf] y configure el `unpackWARs` al establecerlo en `false`.

>[!NOTE]
>
>Si ha configurado Tomcat para incluir [!DNL commons-logging.jar] en la ruta de clase del sistema (no necesaria para el servidor DRM de Primetime para flujo protegido), debe configurar el registro común para utilizar Log4J.

El servidor utiliza opcionalmente una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux para obtener un rendimiento óptimo. Puede copiar la biblioteca adecuada para su plataforma desde [!DNL thirdparty/cryptoj/]*plataforma* a una ubicación especificada por el `PATH` variable de entorno o `LD_LIBRARY_PATH` en Linux.

>[!NOTE]
>
>Solo debe utilizar la versión de 64 bits si tanto el sistema operativo como el JDK admiten 64 bits. De lo contrario, debe utilizar la versión de 32 bits.
