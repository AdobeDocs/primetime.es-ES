---
description: Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe habilitarlos. El usuario puede activar o desactivar los subtítulos y seleccionar el formato.
title: Exponer subtítulos cerrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Exponer subtítulos cerrados {#expose-closed-captions}

Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe habilitarlos. El usuario puede activar o desactivar los subtítulos y seleccionar el formato.

Para exponer subtítulos cerrados:

1. Entrada `PTMediaPlayer` objeto, establezca el `closedCaptionDisplayEnabled` propiedad.

   Si el usuario ha habilitado subtítulos opcionales, este paso muestra el texto.

   >[!NOTE]
   >
   >El usuario cliente activa o desactiva los subtítulos mediante la Configuración de accesibilidad de iOS, y esta configuración también proporciona opciones de formato.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` La propiedad está obsoleta. Uso `subtitlesOptions` propiedad de `PTMediaPlayerItem`. Consulte [Exponer subtítulos](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) para utilizar subtítulos cerrados.
