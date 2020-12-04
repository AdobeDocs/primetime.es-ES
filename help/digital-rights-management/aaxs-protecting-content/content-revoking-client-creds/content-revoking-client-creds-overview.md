---
seo-title: Revocando las credenciales del cliente
title: Revocando las credenciales del cliente
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Revocando credenciales de cliente{#revoking-client-credentials}

Bajo ciertas condiciones, es necesario revocar las credenciales de un cliente o comprobar si un conjunto determinado de credenciales ya ha sido revocado. Las credenciales se pueden revocar si las credenciales están comprometidas. Cuando esto ocurra, las licencias ya no se expedirán a los clientes comprometidos.

Adobe mantiene Listas de revocación de certificados (CRL) para revocar clientes comprometidos. El SDK aplica automáticamente estas CRL. Los servidores de licencias pueden restringir aún más a los clientes al rechazar determinadas credenciales de equipo o versiones particulares de DRM y credenciales de tiempo de ejecución. Se puede crear un `RevocationList` y pasarlo al SDK para revocar las credenciales del equipo. Se pueden revocar versiones de DRM/tiempo de ejecución particulares en el nivel de directiva (estableciendo restricciones de módulo en la derecha de reproducción) o globalmente (estableciendo restricciones de módulo en `HandlerConfiguration`).

El análisis de este capítulo se centrará en revocar las credenciales de cliente.
