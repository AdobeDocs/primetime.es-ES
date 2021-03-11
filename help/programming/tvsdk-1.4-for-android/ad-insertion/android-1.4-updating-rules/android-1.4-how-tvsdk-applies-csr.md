---
description: 'TVSDK aplica las reglas de selección creativa de las siguientes maneras '
title: Aplicación de reglas de selección creativa
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Aplicación de reglas de selección creativa{#applying-creative-selection-rules}

TVSDK aplica las reglas de selección creativa de las siguientes maneras:

* TVSDK aplica primero todas las reglas `default`, seguido de las reglas específicas de la zona.
* TVSDK ignora las reglas que no están definidas para el ID de zona actual.
* Una vez que TVSDK aplique las reglas predeterminadas, las reglas específicas de la zona pueden cambiar aún más las prioridades creativas en función de las coincidencias `host` (dominio) del elemento creativo seleccionado por las reglas `default`.

* En el archivo de reglas de ejemplo incluido con reglas de zona adicionales, una vez que TVSDK aplique las reglas `default`, si el dominio creativo M3U8 no contiene [!DNL my.domain.com] ni [!DNL a.bcd.com] y el área publicitaria es `1234`, los elementos creativos se reordenarán y el elemento creativo VPAID de Flash se reproducirá primero si está disponible. De lo contrario, se reproduce un anuncio de MP4, y así sucesivamente hasta JavaScript.

* Si se selecciona un creativo de publicidad que TVSDK no puede reproducir de forma nativa ( [!DNL .mp4], [!DNL .flv], etc.), TVSDK emite una solicitud de reempaquetado.

Tenga en cuenta que los tipos de publicidad que TVSDK puede administrar aún se definen mediante la configuración `validMimeTypes` de `AuditudeSettings`.
