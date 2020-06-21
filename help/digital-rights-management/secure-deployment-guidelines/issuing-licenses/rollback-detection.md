---
description: Si la implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidas de AIR o SWF.
seo-description: Si la implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidas de AIR o SWF.
seo-title: Detección de retroceso
title: Detección de retroceso
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Detección de retroceso {#rollback-detection}

Si la implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidas de AIR o SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de DRM de Primetime no requiere el contador de reversión, se puede ignorar. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio, que se obtiene mediante [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), y el valor de contador actual en una base de datos.

Para obtener más información sobre cómo incrementar y realizar el seguimiento del contador de rollback, consulte Detección de [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) y Rollback.