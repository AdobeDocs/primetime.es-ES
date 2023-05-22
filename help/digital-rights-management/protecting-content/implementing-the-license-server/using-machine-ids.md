---
title: Usar identificadores de equipo
description: Usar identificadores de equipo
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usar identificadores de equipo{#use-machine-identifiers}

Todas las solicitudes de DRM de Adobe Primetime (excepto las solicitudes que admiten la compatibilidad con FRMS) incluyen información sobre el token de equipo que se ha emitido al cliente durante la individualización. El token de equipo incluye un ID de equipo, que es un identificador que se ha asignado durante la individualización. Puede utilizar este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Puede utilizar un identificador de la siguiente manera:

* El `getUniqueId()` El método devuelve una cadena que se ha asignado a un dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambia si el usuario vuelve a dar formato al disco duro y vuelve a individualizar. Este identificador también tiene un valor diferente entre Adobe AIR y el Flash Player de Adobe en distintos navegadores del mismo equipo.
* Si desea contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si el equipo ya se ha visto, obtenga todos los identificadores para un nombre de usuario y llame a `matches()` para comprobar si hay alguna coincidencia. Debido a que el `matches()` debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`Sin embargo, esta opción solo es práctica cuando hay un pequeño número de valores que comparar; por ejemplo, los equipos asociados con un usuario en particular.

