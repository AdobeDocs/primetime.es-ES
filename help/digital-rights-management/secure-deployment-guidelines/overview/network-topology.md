---
title: Introducción a la topología de red
description: Introducción a la topología de red
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Información general {#network-topology-overview}

Después de implementar correctamente Adobe Primetime DRM, debe mantener la seguridad del servidor de producción DRM de Primetime.

>[!NOTE]
>
>Primetime DRM se conocía anteriormente como Acceso de Adobe y, antes de eso, como Flash Access.

Puede usar un *proxy inverso* para garantizar que los usuarios externos e internos tengan a su disposición diferentes conjuntos de URL para las aplicaciones web de DRM de Primetime. *Proxy inverso* es más seguro que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se ejecuta Primetime DRM y esta configuración realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta Primetime DRM. Los usuarios solo pueden acceder al proxy inverso y solo pueden intentar las conexiones URL compatibles con el proxy inverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
