---
title: Introducción a la topología de red
description: Introducción a la topología de red
copied-description: true
exl-id: ca5e8701-f8a3-4125-bb60-bfb9efd5c8f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# Introducción a la topología de red {#network-topology-overview}

Después de implementar correctamente Adobe Access, es importante mantener la seguridad de su entorno. En esta sección se describen las tareas necesarias para mantener la seguridad del servidor de producción de Acceso a Adobe.

Utilice un *proxy inverso* para asegurarse de que los usuarios externos e internos tengan a su disposición diferentes conjuntos de direcciones URL para aplicaciones web de acceso de Adobe. Esta configuración es más segura que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se está ejecutando el acceso al Adobe. El proxy inverso realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta el acceso de Adobe. Los usuarios solo tienen acceso a la red desde el proxy inverso y solo pueden intentar las conexiones URL compatibles con el proxy inverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
