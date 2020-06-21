---
seo-title: Detección de retroceso
title: Detección de retroceso
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Detección de retroceso{#rollback-detection}

Si la implementación de Adobe Access utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda encarecidamente que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidas de AIR o SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de Adobe Access no requiere el contador de reversión, se puede ignorar. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio (obtenido mediante `MachineToken.getMachineId().getUniqueId()`) y el valor de contador actual en una base de datos. Para obtener más información sobre el aumento y el seguimiento del contador de rollback, consulte ClientState en Referencia *de API de* Adobe Access y detección *de* rollback en *Uso del SDK de Adobe Access para la protección de contenido*.
