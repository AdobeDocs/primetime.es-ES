---
title: Información general sobre la topología de red
description: Información general sobre la topología de red
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Información general {#network-topology-overview}

Después de implementar correctamente Adobe Primetime DRM, debe mantener la seguridad del servidor de producción Primetime DRM.

>[!NOTE]
>
>Primetime DRM se conocía anteriormente como Acceso a Adobe y antes de eso, Flash Access.

Puede utilizar un *proxy inverso* para garantizar que los distintos conjuntos de URL para las aplicaciones web de DRM de Primetime estén disponibles para los usuarios externos e internos. *El* proxy inverso es más seguro que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se ejecuta Primetime DRM, y esta configuración realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta Primetime DRM. Los usuarios solo pueden acceder al proxy inverso y solo pueden intentar las conexiones URL que admite el proxy inverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)