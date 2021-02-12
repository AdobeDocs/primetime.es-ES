---
description: Puede habilitar el seguimiento de publicidades del lado del cliente agregando los parámetros pttrackingmode y pttrackingversion a la solicitud de URL del Bootstrap.
seo-description: Puede habilitar el seguimiento de publicidades del lado del cliente agregando los parámetros pttrackingmode y pttrackingversion a la solicitud de URL del Bootstrap.
seo-title: Habilitar el seguimiento de publicidades del lado del cliente
title: Habilitar el seguimiento de publicidades del lado del cliente
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 1%

---


# Habilitar el seguimiento de publicidades del lado del cliente {#enable-client-side-ad-tracking}

Puede habilitar el seguimiento de publicidades en el lado del cliente agregando los parámetros `pttrackingmode` y `pttrackingversion` a la solicitud de URL del Bootstrap.

Con el seguimiento de anuncios del lado del cliente habilitado, también puede recuperar metadatos de seguimiento de anuncios mediante la URL de la API de seguimiento. Para obtener más información, consulte [Parámetros de Consulta](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Para realizar el seguimiento de anuncios del lado del cliente, utilice la URL de la API de seguimiento.

1. Añada los siguientes parámetros de consulta a la URL de solicitud de servidor de manifiesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Por ejemplo:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
