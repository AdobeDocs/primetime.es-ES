---
description: Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.
seo-description: Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.
seo-title: Recuento de equipos al emitir licencias
title: Recuento de equipos al emitir licencias
uuid: 7ba8a8d4-a31f-4f37-82a7-755cfa443544
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Recuento de equipos al emitir licencias {#machine-count-when-issuing-licenses}

Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.

La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) en una base de datos. Cuando se recibe una nueva solicitud, compare el ID de equipo de la solicitud con los ID de equipo conocidos mediante [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza una comparación de ID para determinar si los ID representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de máquina. Por ejemplo, si se permite a los usuarios cinco equipos en su dominio, puede buscar en la base de datos los ID de equipo asociados al nombre de usuario del usuario y obtener un pequeño conjunto de datos para la comparación.

Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En este caso, se puede usar [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) . Sin embargo, este ID no puede ser el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®.

>[!NOTE]
>
>El ID no sobrevive si el usuario cambia el formato del disco duro.