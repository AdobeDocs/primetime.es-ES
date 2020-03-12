---
description: Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos opcionales y seleccionar el formato.
seo-description: Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos opcionales y seleccionar el formato.
seo-title: Exponer subtítulos opcionales
title: Exponer subtítulos opcionales
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# Exponer subtítulos opcionales {#expose-closed-captions}

Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos opcionales y seleccionar el formato.

Para exponer subtítulos opcionales:

1. En `PTMediaPlayer` objeto, establezca la `closedCaptionDisplayEnabled` propiedad.

   Si el usuario ha activado los subtítulos opcionales, este paso muestra el texto.

   >[!NOTE]
   >
   >El usuario cliente activa o desactiva los subtítulos opcionales mediante la Configuración de accesibilidad de iOS y esta configuración también proporciona opciones de formato.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` está en desuso. Utilice `subtitlesOptions` la propiedad de `PTMediaPlayerItem`. Consulte [Exponer subtítulos](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) para utilizar subtítulos opcionales.