---
description: Si su implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidos de AIR o SWF.
title: Detección de reversión
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Detección de reversión {#rollback-detection}

Si su implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidos de AIR o SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de DRM de Primetime no requiere el contador de reversión, se puede ignorar. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio, que se obtiene mediante [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), y el valor de contador actual en una base de datos.

Para obtener más información sobre cómo incrementar y rastrear el contador de reversión, consulte [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) y Detección de reversión.