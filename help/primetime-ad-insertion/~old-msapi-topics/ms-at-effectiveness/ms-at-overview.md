---
description: La mayoría de los anunciantes requieren información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus publicidades. El método más eficaz es hacer que el reproductor cliente envíe informes mientras reproduce las publicidades, pero el servidor de manifiesto también admite el seguimiento de anuncios híbridos y del lado del servidor.
seo-description: La mayoría de los anunciantes requieren información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus publicidades. El método más eficaz es hacer que el reproductor cliente envíe informes mientras reproduce las publicidades, pero el servidor de manifiesto también admite el seguimiento de anuncios híbridos y del lado del servidor.
seo-title: Seguimiento de publicidades
title: Seguimiento de publicidades
uuid: 184b8c36-5e51-42a7-b905-53f2b7b15e49
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Seguimiento de publicidad {#ad-tracking}

La mayoría de los anunciantes requieren información detallada sobre cuándo, durante cuánto tiempo y con qué éxito se vieron sus publicidades. El método más eficaz es hacer que el reproductor cliente envíe informes mientras reproduce las publicidades, pero el servidor de manifiesto también admite el seguimiento de anuncios híbridos y del lado del servidor.

Al habilitar el seguimiento de publicidad, el cliente especifica uno de los siguientes enfoques:

* **Del** lado del clienteJunto con la lista de reproducción vinculada con la publicidad, el servidor envía al cliente una estructura JSON, VMAP o en manifiesto que especifica eventos de seguimiento y direcciones URL. Este método es compatible con Interactive Advertising Bureau (IAB)

* **Del** lado del servidorEl cliente no participa en el seguimiento de anuncios. El servidor envía la información de seguimiento de publicidad que pueda. Los datos de seguimiento se calculan únicamente en el lado del servidor y es posible que no coincidan con la actividad de reproducción del lado del cliente. Por ejemplo, si un usuario final no vista toda la publicidad, después de que se entreguen los segmentos, el servidor seguirá considerando que la publicidad se está reproduciendo.

* **** HíbridoEs como el seguimiento del lado del cliente, pero el cliente envía sus informes al servidor de manifiesto, que los reenvía a las direcciones URL correspondientes. Los anunciantes reciben la misma información que con el seguimiento del lado del cliente. Este modo se adapta a los clientes que se ejecutan con acceso a Internet restringido.