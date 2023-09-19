---
title: Información general sobre la implementación de Adobe Access Server para flujo protegido
description: Información general sobre la implementación de Adobe Access Server para flujo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Información general sobre la implementación de Adobe Access Server para flujo protegido {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implementar Adobe Access Server para flujo protegido, asegúrese de que ha instalado las versiones de Java y Tomcat que se indican en la sección Requisitos.

El paquete Adobe Access Server para transmisión por secuencias protegida incluye [!DNL flashaccesserver.war]. Para implementar este archivo WAR, cópielo en el de Tomcat [!DNL webapps] directorio. Si ha implementado previamente el archivo WAR, es posible que tenga que eliminar manualmente el directorio WAR desempaquetado ( [!DNL flashaccessserver] en Tomcat&#39;s [!DNL webapps] directorio). Para evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] archivo en Tomcat&#39;s [!DNL conf] y establezca el `unpackWARs` atribuir a `false`.

>[!NOTE]
>
>Si ha configurado Tomcat para incluir [!DNL commons-logging.jar] en la ruta de clase del sistema (no necesaria para Adobe Access Server para flujo protegido), el registro común debe configurarse para utilizar Log4J.

El servidor utiliza opcionalmente una biblioteca específica de la plataforma ( [!DNL jsafe.dll] en Microsoft Windows o [!DNL libjsafe.so] en Linux) para obtener un rendimiento óptimo. Copie la biblioteca adecuada para su plataforma desde [!DNL thirdparty/cryptoj/]*plataforma* a una ubicación especificada por el `PATH` variable de entorno (o `LD_LIBRARY_PATH` en Linux).

>[!NOTE]
>
>La versión de 64 bits solo debe utilizarse si el sistema operativo y el JDK admiten 64 bits; de lo contrario, utilice la versión de 32 bits.
