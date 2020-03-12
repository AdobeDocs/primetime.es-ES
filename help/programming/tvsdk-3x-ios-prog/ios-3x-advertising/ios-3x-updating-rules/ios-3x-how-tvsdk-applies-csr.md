---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: Aplicar reglas de selección creativa
title: Aplicar reglas de selección creativa
uuid: 2f009776-201c-418e-aa8f-cb409d0046d8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Aplicar reglas de selección creativa {#apply-creative-selection-rules}

TVSDK aplica las reglas de selección creativa de las siguientes formas:

* TVSDK aplica primero todas `default` las reglas, seguido de las reglas específicas de la zona.
* TVSDK ignora las reglas que no están definidas para el ID de zona actual.
* Una vez que TVSDK aplique las reglas predeterminadas, las reglas específicas de la zona pueden cambiar aún más las prioridades creativas en función de las coincidencias `host` (dominio) del elemento creativo seleccionado por las `default` reglas.

* En el archivo de reglas de ejemplo incluido con reglas de zona adicionales, una vez que TVSDK aplique las `default` reglas, si el dominio creativo M3U8 no contiene [!DNL my.domain.com] o [!DNL a.bcd.com] y la zona de publicidad es `1234`, los elementos creativos se reordenarán y el elemento creativo Flash VPAID se reproducirá primero si está disponible. De lo contrario, se reproduce un anuncio MP4 y así sucesivamente hasta JavaScript.

* Si se selecciona un elemento creativo de publicidad que TVSDK no puede reproducir de forma nativa ( [!DNL .mp4], [!DNL .flv], etc.), TVSDK emite una solicitud de reempaquetado.

Tenga en cuenta que los tipos de publicidad que TVSDK puede gestionar aún se definen mediante la `validMimeTypes` configuración de `AuditudeSettings`.