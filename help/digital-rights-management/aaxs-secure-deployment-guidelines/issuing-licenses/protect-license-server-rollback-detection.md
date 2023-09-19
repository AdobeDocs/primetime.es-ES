---
title: Detección de reversión
description: Detección de reversión
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Detección de reversión {#rollback-detection}

Si la implementación de Adobe Access utiliza reglas empresariales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda encarecidamente que el servidor realice un seguimiento del contador de reversiones y utilice la lista de permitidos de AIR o SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de Acceso a Adobe no requiere el contador de reversiones, se puede omitir. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio obtenido mediante `MachineToken.getMachineId().getUniqueId()`: y el valor del contador actual de una base de datos. Para obtener más información sobre cómo incrementar y realizar un seguimiento del contador de reversiones, vea ClientState en *Referencia de API de acceso de Adobe* y *Detección de reversión* in *Uso del SDK de acceso a Adobe para proteger el contenido*.
