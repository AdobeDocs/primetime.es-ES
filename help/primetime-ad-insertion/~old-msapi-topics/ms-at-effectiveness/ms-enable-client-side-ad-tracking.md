---
description: Puede habilitar el seguimiento de anuncios del lado del cliente añadiendo los parámetros pttrackingmode y pttrackingversion a la solicitud de URL del Bootstrap.
title: Habilitar el seguimiento de anuncios del lado del cliente
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Habilitar el seguimiento de anuncios del lado del cliente {#enable-client-side-ad-tracking}

Puede habilitar el seguimiento de anuncios del lado del cliente añadiendo la variable `pttrackingmode` y `pttrackingversion` parámetros para la solicitud de URL del Bootstrap.

Con el seguimiento de anuncios del lado del cliente habilitado, también puede recuperar los metadatos de seguimiento de anuncios mediante la URL de la API de seguimiento. Para obtener más información, consulte [Parámetros de consulta](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Para realizar el seguimiento de anuncios del lado del cliente, utilice la URL de la API de seguimiento.

1. Agregue los siguientes parámetros de consulta a la dirección URL de solicitud del servidor de manifiesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Por ejemplo:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
