---
title: Revocación de las credenciales del cliente
description: Revocación de las credenciales del cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Revocando las credenciales del cliente{#revoking-client-credentials}

En determinadas condiciones es necesario revocar las credenciales de un cliente o comprobar si un conjunto determinado de credenciales ya se ha revocado. Las credenciales se pueden revocar si las credenciales están comprometidas. Cuando esto ocurra, ya no se expedirán licencias a clientes comprometidos.

Adobe mantiene listas de revocación de certificados (CRL) para revocar clientes comprometidos. El SDK aplica automáticamente estas CRL. Los servidores de licencias pueden restringir aún más a los clientes al rechazar credenciales de equipo concretas o versiones particulares de DRM y credenciales de tiempo de ejecución. Se puede crear un `RevocationList` que se puede pasar al SDK para revocar las credenciales del equipo. Las versiones específicas de DRM/tiempo de ejecución se pueden revocar a nivel de directiva (estableciendo restricciones de módulo en la derecha de reproducción) o globalmente (estableciendo restricciones de módulo en `HandlerConfiguration`).

La discusión en este capítulo se centrará en revocar las credenciales del cliente.
