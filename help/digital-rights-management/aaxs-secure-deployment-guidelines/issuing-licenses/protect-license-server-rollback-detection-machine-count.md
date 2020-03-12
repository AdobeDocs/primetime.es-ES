---
seo-title: Recuento de equipos al emitir licencias
title: Recuento de equipos al emitir licencias
uuid: d57f8b0b-0363-4b26-bd71-76f4abe5b68f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Recuento de equipos al emitir licencias{#machine-count-when-issuing-licenses}

Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario. La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el `MachineId.getBytes()` método en una base de datos. Cuando se recibe una nueva solicitud, compare el ID de equipo de la solicitud con los ID de equipo conocidos que utilizan `MachineId.matches()`.

`MachineId.matches()` realiza una comparación de ID para determinar si representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de máquina con los que comparar. Por ejemplo, si se permite a un usuario cinco equipos dentro de su dominio, puede buscar en la base de datos los ID de equipo asociados con el nombre de usuario del usuario y obtener un pequeño conjunto de datos para comparar.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. Sin embargo, en estos casos `MachineId.getUniqueID()` se puede utilizar este ID no será el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®, y no sobrevivirá si el usuario cambia el formato de su disco duro.

Para obtener más información `MachineToken.getMachineId()`y `MachineId.matches()`información, consulte la Referencia *de la API de* Adobe Access.
