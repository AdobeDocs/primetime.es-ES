---
description: Para que los subtítulos estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos y seleccionar el formato.
title: Exponer subtítulos cerrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Exponer subtítulos cerrados {#expose-closed-captions}

Para que los subtítulos estén disponibles para el reproductor cliente, debe activarlos. El usuario puede activar o desactivar los subtítulos y seleccionar el formato.

Para exponer subtítulos cerrados:

1. En el objeto `PTMediaPlayer`, establezca la propiedad `closedCaptionDisplayEnabled`.

   Si el usuario ha habilitado los subtítulos, este paso muestra el texto.

   >[!NOTE]
   >
   >El usuario cliente activa o desactiva los subtítulos mediante la Configuración de accesibilidad de iOS, y esta configuración también proporciona opciones de formato.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` está en desuso. Utilice la propiedad `subtitlesOptions` de `PTMediaPlayerItem`. Consulte [Exponer subtítulos](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) para usar subtítulos cerrados.