---
seo-title: Descripción general de la topología de red
title: Descripción general de la topología de red
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Información general {#network-topology-overview}

Después de implementar correctamente Adobe Primetime DRM, debe mantener la seguridad del servidor de producción Primetime DRM.

>[!NOTE]
>
>Primetime DRM se conocía anteriormente como Adobe Access y antes de eso, Flash Access.

Puede utilizar un *proxy inverso* para garantizar que los usuarios externos e internos tengan disponibles diferentes conjuntos de direcciones URL para las aplicaciones web de DRM de Primetime. *El* proxy inverso es más seguro que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se ejecuta Primetime DRM, y esta configuración realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta Primetime DRM. Los usuarios solo pueden acceder al proxy inverso e intentar únicamente las conexiones URL admitidas por el proxy inverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)