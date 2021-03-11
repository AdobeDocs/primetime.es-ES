---
title: Información general sobre la topología de red
description: Información general sobre la topología de red
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Descripción general de la topología de red {#network-topology-overview}

Después de implementar correctamente Acceso a Adobe, es importante mantener la seguridad de su entorno. En esta sección se describen las tareas necesarias para mantener la seguridad del servidor de producción de Adobe Access.

Utilice un *proxy inverso* para asegurarse de que los distintos conjuntos de direcciones URL para las aplicaciones web de acceso a Adobe están disponibles tanto para los usuarios externos como para los internos. Esta configuración es más segura que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se está ejecutando Adobe Access. El proxy inverso realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta Acceso a Adobe. Los usuarios solo tienen acceso de red al proxy inverso y solo pueden intentar las conexiones URL que admite el proxy inverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

