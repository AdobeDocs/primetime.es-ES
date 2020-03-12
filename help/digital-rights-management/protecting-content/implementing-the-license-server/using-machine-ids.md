---
seo-title: Usar identificadores de máquina
title: Usar identificadores de máquina
uuid: 14eee414-62f1-4a9d-84bd-689ca2271d19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Usar identificadores de máquina{#use-machine-identifiers}

Todas las solicitudes de DRM de Adobe Primetime (a excepción de las solicitudes que admiten la compatibilidad con FMRMS) incluyen información sobre el autentificador del equipo que se ha emitido al cliente durante la individualización. El autentificador del equipo incluye un identificador de equipo, que se ha asignado durante la individualización. Puede utilizar este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Puede utilizar un identificador como se indica a continuación:

* El `getUniqueId()` método devuelve una cadena que se ha asignado a un dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambia si el usuario cambia el formato del disco duro y vuelve a individualizarse. Este identificador también tiene un valor diferente entre Adobe AIR y Adobe Flash Player en distintos navegadores del mismo equipo.
* Si desea contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si la máquina ya se ha visto antes, obtenga todos los identificadores de un nombre de usuario y llame `matches()` para comprobar si hay alguna coincidencia. Dado que el `matches()` método debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`, esta opción sólo es práctica cuando hay un pequeño número de valores que comparar; por ejemplo, los equipos asociados a un usuario en particular.

