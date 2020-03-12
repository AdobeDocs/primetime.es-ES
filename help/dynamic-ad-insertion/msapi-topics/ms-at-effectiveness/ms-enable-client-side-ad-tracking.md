---
description: Puede habilitar el seguimiento de publicidades del lado del cliente agregando los parámetros pttrackingmode y pttrackingversion a la solicitud de URL de Bootstrap.
seo-description: Puede habilitar el seguimiento de publicidades del lado del cliente agregando los parámetros pttrackingmode y pttrackingversion a la solicitud de URL de Bootstrap.
seo-title: Habilitar el seguimiento de publicidades del lado del cliente
title: Habilitar el seguimiento de publicidades del lado del cliente
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Habilitar el seguimiento de publicidades del lado del cliente {#enable-client-side-ad-tracking}

Puede habilitar el seguimiento de publicidades del lado del cliente agregando los parámetros `pttrackingmode` y `pttrackingversion` a la solicitud de URL de Bootstrap.

Con el seguimiento de anuncios del lado del cliente habilitado, también puede recuperar metadatos de seguimiento de anuncios mediante la URL de la API de seguimiento. Para obtener más información, consulte Parámetros [de consulta](../../msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Para realizar el seguimiento de anuncios del lado del cliente, utilice la URL de la API de seguimiento.

1. Agregue los siguientes parámetros de consulta a la URL de solicitud del servidor de manifiesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Por ejemplo:

```
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
