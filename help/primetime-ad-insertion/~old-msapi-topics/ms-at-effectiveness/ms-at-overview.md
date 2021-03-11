---
description: La mayoría de los anunciantes requieren información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus anuncios. El enfoque más eficiente es hacer que el reproductor cliente envíe informes mientras reproduce los anuncios, pero el servidor de manifiestos también admite el seguimiento de anuncios híbridos y del lado del servidor.
title: Seguimiento de anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Seguimiento de anuncios {#ad-tracking}

La mayoría de los anunciantes requieren información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus anuncios. El enfoque más eficiente es hacer que el reproductor cliente envíe informes mientras reproduce los anuncios, pero el servidor de manifiestos también admite el seguimiento de anuncios híbridos y del lado del servidor.

Al habilitar el seguimiento de anuncios, el cliente especifica uno de los siguientes enfoques:

* **Lado del cliente** Junto con la lista de reproducción vinculada al anuncio, el servidor envía al cliente una estructura JSON, VMAP o en manifiesto que especifica eventos de seguimiento y direcciones URL. Este método es compatible con Interactive Advertising Bureau (IAB)

* **Servidor** El cliente no participa en el seguimiento de anuncios. El servidor envía la información de seguimiento de anuncios que pueda. Los datos de seguimiento se calculan solo en el servidor y es posible que no coincidan con la actividad de reproducción del lado del cliente. Por ejemplo, si un usuario final no ve el anuncio completo, después de que se envíen los segmentos, el servidor seguirá considerando que se reprodujo el anuncio.

* **** HíbridoEs como el seguimiento del lado del cliente, pero el cliente envía sus informes al servidor de manifiestos, que los reenvía a las direcciones URL apropiadas. Los anunciantes reciben la misma información que con el seguimiento del lado del cliente. Este modo permite a los clientes que se ejecuten con acceso restringido a Internet.