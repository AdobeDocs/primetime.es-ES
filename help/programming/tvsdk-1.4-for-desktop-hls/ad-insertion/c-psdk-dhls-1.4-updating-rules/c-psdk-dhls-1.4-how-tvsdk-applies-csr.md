---
title: Aplicar reglas de selección creativa
description: Aplicar reglas de selección creativa
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Aplicar reglas de selección creativa{#applying-creative-selection-rules}

TVSDK aplica reglas de selección creativa de las siguientes maneras:

* TVSDK aplica todo `default` primero, las reglas, seguidas de las reglas específicas de la zona.
* TVSDK ignora las reglas que no estén definidas para el ID de zona actual.
* Una vez que TVSDK aplica las reglas predeterminadas, las reglas específicas de la zona pueden cambiar aún más las prioridades creativas en función de la `host` (dominio) coincide con el elemento creativo seleccionado por `default` reglas.

* En el archivo de reglas de muestra incluido con reglas de zona adicionales, una vez que TVSDK aplique la variable `default` , si el dominio creativo M3U8 no contiene [!DNL my.domain.com] o [!DNL a.bcd.com] y la zona publicitaria es `1234`, los elementos creativos se reordenan y el elemento creativo VPAID de Flash se reproduce primero si está disponible. De lo contrario, se reproduce un anuncio MP4 y así sucesivamente hasta JavaScript.

* Si se selecciona un creativo de publicidad, TVSDK no puede reproducirlo de forma nativa ( [!DNL .mp4], [!DNL .flv], etc.), TVSDK emite una solicitud de reempaquetado.

Tenga en cuenta que los tipos de anuncios que TVSDK puede administrar siguen definiéndose a través de `validMimeTypes` configuración en `AuditudeSettings`.
