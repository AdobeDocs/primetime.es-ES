---
title: Usar identificadores de máquina
description: Usar identificadores de máquina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usar identificadores de máquina{#use-machine-identifiers}

Todas las solicitudes de Adobe Primetime DRM (excepto las solicitudes que admiten la compatibilidad con FMRMS) incluyen información sobre el token de equipo que se ha emitido al cliente durante la personalización. El token de equipo incluye un ID de equipo, que es un identificador que se ha asignado durante la individualización. Puede utilizar este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Puede utilizar un identificador como se indica a continuación:

* El método `getUniqueId()` devuelve una cadena que se ha asignado a un dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambia si el usuario vuelve a dar formato al disco duro y se vuelve a individualizar. Este identificador también tiene un valor diferente entre Adobe AIR y el Flash Player de Adobe en distintos navegadores del mismo equipo.
* Si desea contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si el equipo se ha visto antes, obtenga todos los identificadores de un nombre de usuario e invoque `matches()` para comprobar si hay alguna coincidencia. Dado que el método `matches()` debe usarse para comparar los valores devueltos por `MachineId.getBytes`, esta opción solo es práctica cuando hay un pequeño número de valores para comparar; por ejemplo, las máquinas asociadas a un usuario en particular.

