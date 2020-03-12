---
description: 'null'
seo-description: 'null'
seo-title: Configure el token XSTS en el reproductor
title: Configure el token XSTS en el reproductor
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b

---


# Configure el token XSTS en el reproductor{#set-the-xsts-token-in-your-player}

En Xbox360, se establece el token asincrónicamente como respuesta al `MediaPlayer.RequestKeyAttribute` evento.

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

