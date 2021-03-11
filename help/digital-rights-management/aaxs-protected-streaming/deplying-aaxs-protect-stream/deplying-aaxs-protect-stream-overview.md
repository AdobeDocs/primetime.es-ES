---
title: Información general sobre la implementación de Adobe Access Server para transmisión protegida
description: Información general sobre la implementación de Adobe Access Server para transmisión protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Información general sobre la implementación de Adobe Access Server para transmisión protegida {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implementar Adobe Access Server para transmisión protegida, asegúrese de que ha instalado las versiones de Java y Tomcat que se enumeran en la sección Requisitos .

El paquete Adobe Access Server para transmisión protegida incluye [!DNL flashaccesserver.war]. Para implementar este archivo WAR, cópielo en el directorio [!DNL webapps] de Tomcat. Si ha implementado anteriormente el archivo WAR, es posible que tenga que eliminar manualmente el directorio WAR desempaquetado ( [!DNL flashaccessserver] en el directorio [!DNL webapps] de Tomcat). Para evitar que Tomcat desempaquete archivos WAR, edite el archivo [!DNL server.xml] en el directorio [!DNL conf] de Tomcat y establezca el atributo `unpackWARs` en `false`.

>[!NOTE]
>
>Si ha configurado Tomcat para incluir [!DNL commons-logging.jar] en la ruta de clase del sistema (no necesario para Adobe Access Server para transmisión protegida), se debe configurar el registro común para utilizar Log4J.

El servidor opcionalmente utiliza una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux) para obtener un rendimiento óptimo. Copie la biblioteca adecuada para su plataforma de [!DNL thirdparty/cryptoj/]*platform* a una ubicación especificada por la variable de entorno `PATH` (o `LD_LIBRARY_PATH` en Linux).

>[!NOTE]
>
>La versión de 64 bits solo debe utilizarse si tanto el sistema operativo como JDK admiten 64 bits; de lo contrario, utilice la versión de 32 bits.

