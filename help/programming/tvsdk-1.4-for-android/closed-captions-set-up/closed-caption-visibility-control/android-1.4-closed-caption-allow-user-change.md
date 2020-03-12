---
description: Este es un ejemplo de cómo crear un botón que permite al usuario seleccionar una pista de subtítulos opcionales.
seo-description: Este es un ejemplo de cómo crear un botón que permite al usuario seleccionar una pista de subtítulos opcionales.
seo-title: Ejemplo Permitir que los usuarios cambien el seguimiento de rótulos
title: Ejemplo Permitir que los usuarios cambien el seguimiento de rótulos
uuid: 4b69d569-0d6e-4388-9fe3-488e2a4d762d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ejemplo: Permitir que los usuarios cambien el seguimiento de rótulos{#example-allow-users-to-change-the-caption-track}

Este es un ejemplo de cómo crear un botón que permite al usuario seleccionar una pista de subtítulos opcionales.

1. Cree un botón sencillo para cambiar la pista de subtítulos opcionales.

   ```xml
      <Button 
     android:id="@+id/selectCC" 
     android:layout_width="wrap_content" 
     android:layout_height="wrap_content" 
     android:layout_alignParentBottom="true" 
     android:layout_alignParentRight="true" 
     android:layout_marginRight="10dp" 
     android:onClick="selectClosedCaptioningClick" 
     android:text="CC" /> 
   ```

1. Convierta la lista de pistas de subtítulos opcionales disponibles en una matriz de cadenas. Las pistas de subtítulos opcionales que tienen actividad (es decir, los canales para los que TVSDK ha descubierto datos) se marcan de forma correspondiente:

   ```java
   /** 
   * Converts the closed captions tracks to a string array. 
   * 
   * @return array of CC tracks 
   */ 
   private String[] getCCsAsArray() { 
       List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); 
       MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); 
       if (currentItem != null) { 
           List<ClosedCaptionsTrack> closedCaptionsTracks = 
             currentItem.getClosedCaptionsTracks(); 
           Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator(); 
           while (iterator.hasNext()) { 
               ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); 
               String isActive = closedCaptionsTrack.isActive() ? " (" + getString(R.string.active)+ ")" : ""; 
               closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName() + isActive); 
           } 
       } 
       return closedCaptionsTracksAsStrings.toArray(new 
       String[closedCaptionsTracksAsStrings.size()]); 
   } 
   ```

1. Cuando el usuario hace clic en el botón, muestra un cuadro de diálogo que enumera todas las pistas de CC predeterminadas.

   ```java
      public void selectClosedCaptioningClick(View view) { 
       Log.i(LOG_TAG + "#selectClosedCaptions", "Displaying closed captions chooser dialog."); 
       final String items[] = getCCsAsArray(); 
       final AlertDialog.Builder ab = new AlertDialog.Builder(this); 
       ab.setTitle(R.string.PlayerControlCCDialogTitle); 
       ab.setSingleChoiceItems(items, selectedClosedCaptionsIndex, new DialogInterface.OnClickListener() { 
           public void onClick(DialogInterface dialog, int whichButton) { 
               // Select the new closed captioning track. 
               MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); 
               ClosedCaptionsTrack desiredClosedCaptionsTrack = currentItem.getClosedCaptionsTracks().get(whichButton); 
               boolean result = currentItem.selectClosedCaptionsTrack(desiredClosedCaptionsTrack); 
               if (result) { 
                   selectedClosedCaptionsIndex = whichButton; 
               } 
               // Dismiss dialog. 
               dialog.cancel(); 
           } 
       }).setNegativeButton(R.string.PlayerControlCCDialogCancel, new DialogInterface.OnClickListener() { 
           public void onClick(DialogInterface dialog, int whichButton) { 
           // Just cancel the dialog. 
           } 
       }); 
       ab.show(); 
   } 
   ```

