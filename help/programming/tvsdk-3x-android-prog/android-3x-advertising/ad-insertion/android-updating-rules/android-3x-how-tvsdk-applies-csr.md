---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: Aplicar reglas de selección creativa
title: Aplicar reglas de selección creativa
uuid: 66e55f95-25ce-4838-b222-63ee34e535d1
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Aplicar reglas de selección creativa {#apply-creative-selection-rules}

TVSDK aplica las reglas de selección creativa de las siguientes formas:

* TVSDK aplica primero todas las reglas `default`, seguidas de las reglas específicas de la zona.
* TVSDK ignora las reglas que no están definidas para el ID de zona actual.
* Una vez que TVSDK aplique las reglas predeterminadas, las reglas específicas de la zona pueden cambiar aún más las prioridades creativas en función de las coincidencias `host` (dominio) del elemento creativo seleccionado por las reglas `default`.

* En el archivo de reglas de ejemplo incluido con reglas de zona adicionales, una vez que TVSDK aplique las reglas `default`, si el dominio creativo M3U8 no contiene `my.domain.com` o `a.bcd.com` y la zona de publicidad sea `1234`, los elementos creativos se reordenarán y el elemento creativo VPAID de Flash se reproducirá primero si está disponible. De lo contrario, se reproduce un anuncio MP4 y así sucesivamente hasta JavaScript.

* Si se selecciona un elemento creativo de publicidad que TVSDK no puede reproducir de forma nativa ( [!DNL .mp4], [!DNL .flv], etc.), TVSDK emite una solicitud de reempaquetado.

Tenga en cuenta que los tipos de publicidad que TVSDK puede administrar aún se definen mediante la configuración `validMimeTypes` de `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

