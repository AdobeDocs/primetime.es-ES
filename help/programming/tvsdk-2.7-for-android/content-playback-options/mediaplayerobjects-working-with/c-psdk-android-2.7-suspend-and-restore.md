---
description: La aplicación debe controlar la suspensión y restauración del MediaPlayer de TVSDK cuando la pantalla de un dispositivo está desactivada y activada.
keywords: SurfaceView;Suspender;Restaurar;BroadcastReceiver
title: Suspender y restaurar MediaPlayer
exl-id: 159f0f4f-2bb7-40a1-9747-be970dfbb04d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Suspender y restaurar MediaPlayer {#suspend-and-restore-mediaplayer}

La aplicación debe controlar la suspensión y restauración del MediaPlayer de TVSDK cuando la pantalla de un dispositivo está desactivada y activada.

Puede gestionar las operaciones de suspensión y restauración en `MediaPlayer` dentro del receptor de difusión de Android para activar o desactivar la pantalla.

TVSDK no puede determinar cuándo un fragmento (o actividad) está en segundo plano o en primer plano. Además, el Android `SurfaceView` no se destruye cuando la pantalla del dispositivo está desactivada (pero la actividad está en pausa). Sin embargo, `SurfaceView` *hace* se destruyen cuando el dispositivo pone la aplicación en segundo plano. TVSDK no puede detectar ninguno de estos cambios, por lo que su aplicación debe gestionarlos.

El siguiente código de ejemplo muestra cómo la aplicación puede controlar la suspensión y restauración del `MediaPlayer` cuando la pantalla del dispositivo está encendida y apagada en el nivel de aplicación:

```java
// Track the state of a fragment to determine if it is PAUSED or RESUMED 
private boolean isActivityPaused = false; 
 
/** 
* Register the broadcast receiver to track screen on/screen off functions triggered from 
device. 
*/ 
private BroadcastReceiver mReceiver = new BroadcastReceiver() { 
    @Override 
    public void onReceive(Context context, Intent intent) { 
 
        // Call suspend when screen is turned off and mediaPlayer is not null and 
        // mediaplayer status is not suspended/Error/Released state. 
        if (intent.getAction().equals(Intent.ACTION_SCREEN_OFF)) { 
            try { 
                if (mediaPlayer != null && 
                  lastKnownStatus != MediaPlayerStatus.ERROR && 
                  lastKnownStatus != MediaPlayerStatus.RELEASED && 
                  lastKnownStatus != MediaPlayerStatus.SUSPENDED) { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOff:", 
                    "Suspending mediaplayer as screen is turned off and mediaPlayer 
                    status is " + lastKnownStatus.toString()); 
                    mediaPlayer.suspend(); 
                } 
                else { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOff:", 
                      "Not suspending mediaplayer since mediaplayer status is " 
                      + lastKnownStatus.toString()); 
                } 
            } catch(MediaPlayerException e) { 
                PrimetimeReference.logger.e(LOG_TAG+"#screenOff:", 
                  "MediaPlayer Exception for suspend() call"); 
            } 
        } 
        else if (intent.getAction().equals(Intent.ACTION_SCREEN_ON)) { 
            // Call restore when the screen is turned on and mediaplayer is not in the  
            // suspended status.  This is for the screen on condition when the device  
            // does not have a lock and turning on the screen immediately brings the  
            // fragment to the foreground. 
            try { 
                if(lastKnownStatus == MediaPlayerStatus.SUSPENDED && !isActivityPaused) { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOn:", 
                      "Restoring mediaplayer since screen is turned on and mediaPlayer status is " 
                      + lastKnownStatus.toString()); 
                    mediaPlayer.restore(); 
                } 
                else { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOn:", 
                      "Not restoring mediaplayer since mediaPlayer status is " 
                      + lastKnownStatus.toString()); 
                } 
            } catch(MediaPlayerException e) { 
                PrimetimeReference.logger.e(LOG_TAG+"#screenOn:", 
                  "MediaPlayer Exception for restore() call"); 
            } 
        } 
    } 
}; 
 
/* 
* Activity or Fragment's onPause() overridden method 
*/ 
@Override 
public void onPause() { 
    PrimetimeReference.logger.i(LOG_TAG + "#onPause", "Player activity paused."); 
 
    // Set the fragment paused status to true when app goes in background. 
    isActivityPaused = true; 
    super.onPause(); 
} 
 
/* 
* Activity or Fragment's onResume() overridden method 
*/ 
@Override 
public void onResume() { 
    super.onResume(); 
 
    /** 
    * When the device has a lock/pin the on resume will be called only after the device 
      is unlocked. 
    * Screen on does not call the onResume() method so we need to handle restore here 
      explicitly. 
    */ 
    if(lastKnownStatus == MediaPlayerStatus.SUSPENDED && isActivityPaused) { 
        try { 
            PrimetimeReference.logger.i(LOG_TAG + "#onResume", 
              "Player restored as activity operations are resumed"); 
            mediaPlayer.restore(); 
        } 
        catch(MediaPlayerException e) { 
            PrimetimeReference.logger.i(LOG_TAG + "#onResume",  
              "Exception occured while restoring mediaPlayer"); 
        } 
    } 
    // Set the fragment paused status to false when app comes in foreground. 
    isActivityPaused = false; 
} 
```
