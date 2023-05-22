---
description: La mayoría de los anunciantes necesitan información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus anuncios. El método más eficaz es que el reproductor del cliente envíe informes a medida que reproduce los anuncios, pero el servidor de manifiestos también admite el seguimiento de anuncios híbridos y del lado del servidor.
title: Seguimiento de anuncios
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Seguimiento de anuncios {#ad-tracking}

La mayoría de los anunciantes necesitan información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus anuncios. El método más eficaz es que el reproductor del cliente envíe informes a medida que reproduce los anuncios, pero el servidor de manifiestos también admite el seguimiento de anuncios híbridos y del lado del servidor.

Al habilitar y rastrear, el cliente especifica uno de los siguientes enfoques:

* **Lado del cliente** Junto con la lista de reproducción vinculada a anuncios, el servidor envía al cliente un JSON, VMAP o una estructura en manifiesto que especifica eventos de seguimiento y direcciones URL. Este método es compatible con Interactive Advertising Bureau (IAB)

* **Lado del servidor** El cliente no participa en el seguimiento de anuncios. El servidor envía la información de seguimiento de anuncios que pueda. Los datos de seguimiento se calculan únicamente en el servidor y es posible que no coincidan con la actividad de reproducción del lado del cliente. Por ejemplo, si un usuario final no ve todo el anuncio, una vez entregados los segmentos, el servidor sigue considerando que se reproduce el anuncio.

* **Híbrido** Esto es similar al seguimiento del lado del cliente, pero el cliente envía sus informes al servidor de manifiestos, que los transmite a las direcciones URL adecuadas. Los anunciantes reciben la misma información que con el seguimiento del lado del cliente. Este modo admite clientes que ejecuten con acceso restringido a Internet.