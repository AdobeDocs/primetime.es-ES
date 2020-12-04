---
seo-title: Introducción a la implementación de Adobe Access Server para flujo continuo protegido
title: Introducción a la implementación de Adobe Access Server para flujo continuo protegido
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Implementación de la descripción general de Adobe Access Server para flujo protegido {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implementar Adobe Access Server para flujo continuo protegido, asegúrese de haber instalado las versiones de Java y Tomcat que aparecen en la sección Requisitos.

El paquete Adobe Access Server para flujo continuo protegido incluye [!DNL flashaccesserver.war]. Para implementar este archivo WAR, cópielo en el directorio [!DNL webapps] de Tomcat. Si ya ha implementado el archivo WAR, es posible que tenga que eliminar manualmente el directorio WAR sin empaquetar ( [!DNL flashaccessserver] en el directorio [!DNL webapps] de Tomcat). Para evitar que Tomcat descomprima archivos WAR, edite el archivo [!DNL server.xml] en el directorio [!DNL conf] de Tomcat y establezca el atributo `unpackWARs` en `false`.

>[!NOTE]
>
>Si ha configurado Tomcat para incluir [!DNL commons-logging.jar] en la ruta de clases del sistema (no es necesario para Adobe Access Server para flujo protegido), el registro de recursos comunes debe configurarse para utilizar Log4J.

El servidor opcionalmente utiliza una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux) para un rendimiento óptimo. Copie la biblioteca adecuada para su plataforma de [!DNL thirdparty/cryptoj/]*platform* a una ubicación especificada por la variable de entorno `PATH` (o `LD_LIBRARY_PATH` en Linux).

>[!NOTE]
>
>La versión de 64 bits solo debe utilizarse si tanto el sistema operativo como JDK admiten 64 bits, de lo contrario se utiliza la versión de 32 bits.

