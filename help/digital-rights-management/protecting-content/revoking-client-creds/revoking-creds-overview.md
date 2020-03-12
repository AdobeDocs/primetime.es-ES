---
seo-title: Información general
title: Información general
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Información general{#overview}

Es posible que deba revocar las credenciales de un cliente o comprobar si un conjunto determinado de credenciales ya se ha revocado bajo determinadas condiciones. Las credenciales se pueden revocar si están comprometidas. Cuando se producen estos problemas, las licencias ya no se otorgan a clientes comprometidos.

Adobe mantiene listas de revocación de certificados (CRL) para revocar clientes comprometidos. El SDK aplica automáticamente estas CRL. Los servidores de licencias pueden restringir aún más a los clientes al rechazar determinadas credenciales de equipo o versiones particulares de DRM y credenciales de tiempo de ejecución. Se `RevocationList` puede crear y pasar un archivo al SDK para revocar las credenciales del equipo. Las versiones de DRM/tiempo de ejecución específicas se pueden revocar en el nivel de directiva DRM estableciendo restricciones de módulo en la derecha de reproducción o globalmente estableciendo restricciones de módulo en la `HandlerConfiguration`.

La discusión se centra en revocar las credenciales de cliente.
