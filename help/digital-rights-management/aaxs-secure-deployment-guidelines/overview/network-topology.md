---
seo-title: Descripción general de la topología de red
title: Descripción general de la topología de red
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Visión general de la topología de red {#network-topology-overview}

Después de implementar correctamente Adobe Access, es importante mantener la seguridad de su entorno. En esta sección se describen las tareas necesarias para mantener la seguridad del servidor de producción de Adobe Access.

Utilice un *proxy inverso* para asegurarse de que los distintos conjuntos de direcciones URL para las aplicaciones Web de Adobe Access están disponibles para los usuarios externos e internos. Esta configuración es más segura que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se ejecuta Adobe Access. El proxy inverso realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta Adobe Access. Los usuarios solo tienen acceso de red al proxy inverso y solo pueden intentar las conexiones URL admitidas por el proxy inverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

