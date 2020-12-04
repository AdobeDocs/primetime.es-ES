---
seo-title: Uso de identificadores de máquina
title: Uso de identificadores de máquina
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Uso de identificadores de máquina{#using-machine-identifiers}

Todas las solicitudes de Adobe Access (excepto las solicitudes que admiten la compatibilidad con FMRMS) contienen información sobre el autentificador del equipo emitido al cliente durante la individualización. El autentificador del equipo contiene un identificador de equipo, que se asigna durante la individualización. Utilice este identificador para contar el número de equipos desde los que un usuario ha solicitado una licencia o se ha unido a un dominio.

Existen dos formas de utilizar el identificador. El método `getUniqueId()` devuelve una cadena asignada al dispositivo durante la individualización. Puede almacenar las cadenas en una base de datos y buscar por identificador. Sin embargo, este identificador cambiará si el usuario cambia el formato del disco duro y vuelve a personalizarlo. Este identificador también tendrá un valor diferente entre Adobe® AIR® y Adobe® Flash® Player en distintos navegadores del mismo equipo.

Para contar los equipos con mayor precisión, puede utilizar `getBytes()` para almacenar el identificador completo. Para determinar si la máquina ya se ha visto antes, obtenga todos los identificadores de un nombre de usuario y llame a `matches()` para comprobar si hay alguna coincidencia. Dado que el método `matches()` debe utilizarse para comparar los valores devueltos por `MachineId.getBytes`, esta opción es sólo práctica cuando hay un pequeño número de valores que comparar (por ejemplo, las máquinas asociadas con un usuario en particular).
