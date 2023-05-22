---
keywords: reglas de selección creativa;AdobeTVSDKConfig
title: Aplicar reglas de selección creativa
description: Aplicar reglas de selección creativa
copied-description: true
exl-id: 30a0b783-cb46-444b-9fe7-63a3bd0c4330
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Aplicar reglas de selección creativa{#apply-creative-selection-rules}

TVSDK aplica reglas de selección creativa de las siguientes maneras:

* TVSDK aplica todo `default` primero, las reglas, seguidas de las reglas específicas de la zona.
* TVSDK ignora las reglas que no estén definidas para el ID de zona actual.
* Una vez que TVSDK aplica las reglas predeterminadas, las reglas específicas de la zona pueden cambiar aún más las prioridades creativas en función de la `host` (dominio) coincide con el elemento creativo seleccionado por `default` reglas.

* En el archivo de reglas de muestra incluido con reglas de zona adicionales, una vez que TVSDK aplique la variable `default` , si el dominio creativo M3U8 no contiene [!DNL my.domain.com] o [!DNL a.bcd.com] y la zona publicitaria es `1234`, los elementos creativos se reordenan y el elemento creativo VPAID de Flash se reproduce primero si está disponible. De lo contrario, se reproduce un anuncio MP4 y así sucesivamente hasta JavaScript.

* Si se selecciona un creativo de publicidad, TVSDK no puede reproducirlo de forma nativa ( [!DNL .mp4], [!DNL .flv], etc.), TVSDK emite una solicitud de reempaquetado.

Tenga en cuenta que los tipos de anuncios que TVSDK puede administrar siguen definiéndose a través de `validMimeTypes` configuración en `AuditudeSettings`.
