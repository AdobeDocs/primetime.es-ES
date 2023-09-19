---
title: Uso de identificadores de equipo
description: Uso de identificadores de equipo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Uso de identificadores de equipo{#using-machine-identifiers}

Todas las solicitudes de acceso de Adobe (excepto las solicitudes que admiten la compatibilidad con FRMS) contienen información sobre el token de equipo emitido al cliente durante la individualización. El token de equipo contiene un ID de equipo, un identificador asignado durante la individualización. Utilice este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Existen dos formas de utilizar el identificador. El `getUniqueId()` El método devuelve una cadena asignada al dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambiará si el usuario vuelve a dar formato al disco duro y vuelve a individualizar. Este identificador también tendrá un valor diferente entre Adobe® AIR® y Adobe ® Flash ® Player en exploradores diferentes del mismo equipo.

Para contar las máquinas con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si el equipo ya se ha visto antes, obtenga todos los identificadores para un nombre de usuario y llame a `matches()` para comprobar si hay alguna coincidencia. Debido a que el `matches()` debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`Sin embargo, esta opción solo es práctica cuando hay un pequeño número de valores para comparar (por ejemplo, los equipos asociados con un usuario en particular).
