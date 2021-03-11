---
title: Establezca el token XSTS en el reproductor
description: Establezca el token XSTS en el reproductor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Establezca el token XSTS en su reproductor{#set-the-xsts-token-in-your-player}

En Xbox360, establece el token asincrónicamente en respuesta al evento `MediaPlayer.RequestKeyAttribute`.

Establezca el token XSTS.

La aplicación de ejemplo incluida con el software muestra cómo configurar el token XSTS en el reproductor. Este es el fragmento de código relevante del reproductor de muestra:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

