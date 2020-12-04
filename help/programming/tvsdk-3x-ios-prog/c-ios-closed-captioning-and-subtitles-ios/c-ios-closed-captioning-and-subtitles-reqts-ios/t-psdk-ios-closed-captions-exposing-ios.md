---
description: Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos opcionales y seleccionar el formato.
seo-description: Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos opcionales y seleccionar el formato.
seo-title: Exponer subtítulos opcionales
title: Exponer subtítulos opcionales
uuid: 7057014a-b14a-4790-8f7f-37d7a1fb8194
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Exponer subtítulos cerrados {#expose-closed-captions}

Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos opcionales y seleccionar el formato.

Para exponer subtítulos opcionales:

1. En el objeto `PTMediaPlayer`, establezca la propiedad `closedCaptionDisplayEnabled`.

   Si el usuario ha activado los subtítulos opcionales, este paso muestra el texto.

   >[!NOTE]
   >
   >El usuario cliente activa o desactiva los subtítulos opcionales mediante la Configuración de accesibilidad de iOS y esta configuración también proporciona opciones de formato.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` está en desuso. Utilice la propiedad `subtitlesOptions` de `PTMediaPlayerItem`. Consulte [Exponer subtítulos](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) para utilizar subtítulos opcionales.