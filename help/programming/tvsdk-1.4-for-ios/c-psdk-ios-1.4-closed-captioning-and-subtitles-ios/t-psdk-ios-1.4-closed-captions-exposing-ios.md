---
description: Para que los subtítulos cerrados estén disponibles para el reproductor cliente, debe habilitarlos. El usuario puede activar o desactivar los subtítulos y seleccionar el formato.
title: Exponer subtítulos cerrados
exl-id: 57168c6e-a958-4a89-b22b-0c9f1cab3a49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
   >`closedCaptionDisplayEnabled` La propiedad está obsoleta. Uso `subtitlesOptions` propiedad de `PTMediaPlayerItem`. Consulte [Exponer subtítulos](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) para utilizar subtítulos cerrados.
