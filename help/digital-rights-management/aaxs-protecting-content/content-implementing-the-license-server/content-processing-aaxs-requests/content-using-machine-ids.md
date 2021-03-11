---
title: Uso de identificadores de máquina
description: Uso de identificadores de máquina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Uso de identificadores de máquina{#using-machine-identifiers}

Todas las solicitudes de acceso a Adobe (excepto las solicitudes que admiten la compatibilidad con FMRMS) contienen información sobre el token de equipo emitido al cliente durante la personalización. El token de equipo contiene un ID de equipo, un identificador asignado durante la individualización. Utilice este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Existen dos formas de utilizar el identificador. El método `getUniqueId()` devuelve una cadena asignada al dispositivo durante la personalización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambiará si el usuario cambia el formato del disco duro y vuelve a individualizarse. Este identificador también tendrá un valor diferente entre Adobe® AIR® y Adobe® Flash® Player en distintos navegadores del mismo equipo.

Para contar máquinas con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si el equipo se ha visto antes, obtenga todos los identificadores de un nombre de usuario e invoque `matches()` para comprobar si hay alguna coincidencia. Dado que el método `matches()` debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`, esta opción solo es práctica cuando hay un pequeño número de valores que comparar (por ejemplo, las máquinas asociadas a un usuario en particular).
