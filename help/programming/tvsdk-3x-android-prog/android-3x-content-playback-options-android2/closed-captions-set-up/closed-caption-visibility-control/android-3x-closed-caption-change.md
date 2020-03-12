---
description: Este procedimiento es un ejemplo de cómo crear un botón que permite al usuario seleccionar una pista de subtítulos opcionales.
seo-description: Este procedimiento es un ejemplo de cómo crear un botón que permite al usuario seleccionar una pista de subtítulos opcionales.
seo-title: Permitir que los usuarios cambien el seguimiento de rótulos
title: Permitir que los usuarios cambien el seguimiento de rótulos
uuid: 5a6d33f2-cece-48f6-8a68-fe76d9d2a950
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Permitir que los usuarios cambien el seguimiento de rótulos {#allow-users-to-change-the-caption-track}

Este procedimiento es un ejemplo de cómo crear un botón que permite al usuario seleccionar una pista de subtítulos opcionales.

1. Cree un botón para cambiar la pista de subtítulos opcionales.

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

1. Convierta la lista de pistas de subtítulos opcionales disponibles en una matriz de cadenas.

   Las pistas de subtítulos cerrados que tienen actividad, es decir, los canales para los que TVSDK ha descubierto datos, se marcan de manera acorde.

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
               String isActive = closedCaptionsTrack.isActive() ? " (" +  
                 getString(R.string.active)+ ")" : ""; 
               closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName() +  
                 isActive); 
           } 
       } 
       return closedCaptionsTracksAsStrings. 
         toArray(new String[closedCaptionsTracksAsStrings.size()]); 
   } 
   ```

1. Cuando el usuario hace clic en el botón, muestra un cuadro de diálogo que enumera todas las pistas de subtítulos opcionales predeterminadas.

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
               ClosedCaptionsTrack desiredClosedCaptionsTrack =  
                 currentItem.getClosedCaptionsTracks().get(whichButton); 
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
