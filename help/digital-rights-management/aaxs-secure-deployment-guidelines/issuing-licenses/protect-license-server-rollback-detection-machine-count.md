---
title: Recuento de máquinas al emitir licencias
description: Recuento de máquinas al emitir licencias
copied-description: true
exl-id: de052e98-8ae3-4e12-8f77-787293edda39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Recuento de máquinas al emitir licencias{#machine-count-when-issuing-licenses}

Si las reglas empresariales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los identificadores de equipo asociados al usuario. La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el `MachineId.getBytes()` en una base de datos. Cuando llega una nueva solicitud, compare el ID de equipo de la solicitud con los ID de equipo conocidos mediante `MachineId.matches()`.

`MachineId.matches()` realiza una comparación de los ID para determinar si representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de equipo con los que comparar. Por ejemplo, si a un usuario se le permiten cinco equipos dentro de su dominio, puede buscar en la base de datos los ID de equipo asociados con el nombre de usuario del usuario y obtener un pequeño conjunto de datos con los que comparar.

>[!NOTE]
>
>Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En tales casos `MachineId.getUniqueID()` no obstante, este ID no será el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR® y no se conservará si el usuario vuelve a dar formato a su disco duro.

Para obtener más información acerca de `MachineToken.getMachineId()`y `MachineId.matches()`, consulte la *Referencia de API de acceso de Adobe*.
