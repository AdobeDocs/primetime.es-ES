---
title: Establezca el token XSTS en su reproductor
description: Establezca el token XSTS en su reproductor
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Establezca el token XSTS en su reproductor{#set-the-xsts-token-in-your-player}

En Xbox360, el token se establece de forma asíncrona en respuesta a la `MediaPlayer.RequestKeyAttribute` evento.

Establezca el token XSTS.

La aplicación de ejemplo incluida con el software muestra cómo establecer el token XSTS en el reproductor. Este es el fragmento de código relevante del reproductor de muestra:

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

