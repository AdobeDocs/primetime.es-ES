---
title: Recuento de máquinas al expedir licencias
description: Recuento de máquinas al expedir licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Recuento de máquinas al emitir licencias{#machine-count-when-issuing-licenses}

Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario. La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el método `MachineId.getBytes()` en una base de datos. Cuando llega una nueva solicitud, compare el ID del equipo de la solicitud con los ID del equipo conocidos mediante `MachineId.matches()`.

`MachineId.matches()` realiza una comparación de ID para determinar si representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de equipo con los que comparar. Por ejemplo, si a un usuario se le permiten cinco equipos dentro de su dominio, puede buscar en la base de datos los ID de equipo asociados al nombre de usuario del usuario y obtener un pequeño conjunto de datos con los que compararlos.

>[!NOTE]
>
>Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En estos casos se puede utilizar `MachineId.getUniqueID()`, sin embargo, este ID no será el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®, y no sobrevivirá si el usuario cambia el formato de su disco duro.

Para obtener más información sobre `MachineToken.getMachineId()`y `MachineId.matches()`, consulte la *Referencia de la API de acceso al Adobe*.
