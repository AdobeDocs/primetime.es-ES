---
title: Selección de las pistas de audio
description: Selección de las pistas de audio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Selección de las pistas de audio{#select-the-audio-tracks}

Para seleccionar pistas de audio para enlazar audio en tiempo de ejecución, implemente [IAAConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IAAConfig.html).

| Para... | Llamar a... |
|---|---|
| Obtener una lista de las pistas de AA disponibles | [getAudioTracks()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#getAudioTracks()) |
| Obtener la pista seleccionada actualmente | [getSelectedAudioTrack()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#getSelectedAudioTrack()) |
| Seleccionar una pista AA | [selectAlternateAudioTrack()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#selectAlternateAudioTrack(int)) |

El siguiente ejemplo de código ilustra cómo la implementación de referencia obtiene las pistas de audio del TVSDK y asigna la pista seleccionada al elemento de medios asociado:

```java
/** 
 * Displays a chooser dialog, allowing the user to select the desired 
 * alternate audio track. 
 */ 
private void displayAlternateAudioDialog() { 
    PrimetimeReference.logger.i(LOG_TAG + "#selectAlternateAudio", 
      "Displaying alternate audio chooser dialog."); 
    final int selectedAlternateAudio = aaManager.getSelectedAudioTrackIndex(); 
    if (selectedAlternateAudio != AAManagerOn.INVALID_AUDIO_TRACK) { 
        final String items[] = aaManager.getAudioTracks(); 
        new AlertDialog.Builder(getActivity()) 
          .setTitle(R.string.PlayerControlAADialogTitle) 
          .setSingleChoiceItems(items, selectedAlternateAudio, 
          new DialogInterface.OnClickListener() { 
              public void onClick(DialogInterface dialog, int whichButton) { 
                  boolean result =  
                    aaManager.selectAlternateAudioTrack(whichButton); 
                  if (result) { 
                      PrimetimeReference.logger.i(LOG_TAG 
                                                  + "#selectAlternateAudio", 
                                                  "Audio track selection successful"); 
                  } else { 
                      PrimetimeReference.logger.i(LOG_TAG 
                                            + "#selectAlternateAudio", 
                                            "Audio track selection failed"); 
                  } 
                  // Dismiss dialog. 
                  dialog.cancel(); 
              } 
          }).setNegativeButton(R.string.PlayerControlCCDialogCancel, 
                               new DialogInterface.OnClickListener() { 
              public void onClick(DialogInterface dialog, 
                                    int whichButton) { 
                                // Just cancel the dialog. 
              } 
          }).show(); 
 
    } else { 
        PrimetimeReference.logger.i(LOG_TAG + "#selectAlternateAudioFailed", 
                "Unable to detect the currently selected audio track."); 
        Toast.makeText(getActivity(), 
                "Unable to detect the currently selected audio track", 
                Toast.LENGTH_SHORT).show(); 
    } 
} 
```
