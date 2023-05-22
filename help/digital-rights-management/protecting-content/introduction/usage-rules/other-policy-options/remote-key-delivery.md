---
title: Entrega de claves iOS remotas y locales
description: Entrega de claves iOS remotas y locales
copied-description: true
exl-id: becc2d3f-39f3-40ee-b980-7dfbbe6f569d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Entrega de claves iOS remotas y locales {#remote-and-local-ios-key-delivery}

Adobe Primetime admite las siguientes opciones para la entrega de claves a clientes de iOS:

* **Remoto** : Funciona según se especifica en la especificación de flujo en directo HTTP (HLS); el manifiesto M3U8 especifica una ruta HTTPS que incluye una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados del flujo. Cuando especifique `Remote` en la directiva DRM de Primetime, el dispositivo cliente debe conectarse a un servidor HTTPS remoto para obtener una clave AES.

* **Local** - Cuando especifique `Local` en el DRM de Primetime, en lugar de conectarse a Internet/red para la clave AES, se incrusta un servidor HTTPS local en la aplicación de iOS, que luego administra todas las solicitudes de clave AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación IP. El desarrollador de aplicaciones no requiere ninguna intervención.

La entrega de claves remotas se habilita a través de la directiva DRM de Primetime que se utiliza para empaquetar contenido. Si desea cambiar esta configuración, debe volver a empaquetar el contenido. Si activa la entrega de claves remotas, debe implementar un Servidor de claves DRM de Primetime que pueda administrar las solicitudes de claves de los clientes de iOS. Sin embargo, no se han realizado cambios en el flujo de trabajo para clientes de otras plataformas.

>[!NOTE]
>
>La selección Entrega de claves solo afecta a los clientes de iOS. Todos los demás dispositivos que utilizan contenido HLS, como Android y Primetime en el escritorio (Flash Player), siempre utilizan `Local` entrega de claves, incluso si `Remote` se ha especificado.
