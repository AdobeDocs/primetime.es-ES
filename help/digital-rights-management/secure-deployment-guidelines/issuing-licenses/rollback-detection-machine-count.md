---
description: Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.
title: Recuento de máquinas al expedir licencias
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Recuento de máquinas al emitir licencias {#machine-count-when-issuing-licenses}

Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.

La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) en una base de datos. Cuando se recibe una nueva solicitud, compare el ID del equipo de la solicitud con los ID del equipo conocidos mediante el uso de [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza una comparación de ID para determinar si los ID representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de equipo. Por ejemplo, si se permite a los usuarios cinco equipos en su dominio, puede buscar en la base de datos los ID de equipo asociados al nombre de usuario del usuario y obtener un pequeño conjunto de datos para compararlos.

Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En este caso, se puede utilizar [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()). Sin embargo, este ID no puede ser el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®.

>[!NOTE]
>
>El ID no sobrevive si el usuario cambia el formato del disco duro.