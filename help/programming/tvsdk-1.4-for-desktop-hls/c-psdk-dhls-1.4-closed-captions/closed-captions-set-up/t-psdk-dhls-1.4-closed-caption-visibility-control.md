---
description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.
seo-description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.
seo-title: Control de la visibilidad de los subtítulos opcionales
title: Control de la visibilidad de los subtítulos opcionales
uuid: 360d1158-67d9-40d9-b4b6-8ef46f9d73c0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Control de la visibilidad de los subtítulos opcionales{#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.

>[!TIP]
>
>Si se muestra texto de subtítulos opcionales cuando el reproductor entra en el modo de búsqueda, el texto ya no se muestra una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK muestra el siguiente texto de subtítulos opcionales en el vídeo después de la posición de búsqueda final.

>[!NOTE]
>
>Los valores de visibilidad de los subtítulos cerrados se definen en `ClosedCaptionsVisibility`.
>
>
```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```

1. Espere a que el `MediaPlayer` estado PREPARADO (consulte [Esperar un estado](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)válido).
1. Para obtener la configuración de visibilidad actual de los subtítulos cerrados, utilice el método getter en `MediaPlayer`, que devuelve un valor de visibilidad.

   ```
   public function get ccVisibility():String
   ```

1. Para cambiar la visibilidad de los subtítulos cerrados, utilice el método setter, pasando un valor de visibilidad de `ClosedCaptionsVisibility`.

   Por ejemplo:

   ```
   public function set ccVisibility(value:String):void
   ```

1. Defina una lista desplegable.

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. Defina una matriz enlazable de pistas de subtítulos opcionales.

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. Configure los oyentes.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   Para eliminar los oyentes del código de destrucción:

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. Cree y actualice la lista cuando un usuario elija una opción en la lista.

   ```
   private function onCCTrackChange(event:IndexChangeEvent):void { 
       var ccTrackIndex:int = event.newIndex; 
       var ccTracks:Vector.<ClosedCaptionsTrack> =  
         _player.currentItem.closedCaptionsTracks; 
       if (ccTrackIndex == 0) { 
           _player.ccVisibility = MediaPlayer.INVISIBLE; 
       } 
       else if (ccTrackIndex <= _ccTracks.length) { 
           var index:Number = findFromActiveIndex(ccTracks, ccTrackIndex - 1); 
           _player.currentItem.selectClosedCaptionsTrack(ccTracks[index]); 
           _player.ccVisibility = MediaPlayer.VISIBLE; 
       } 
   } 
   
   private function findFromActiveIndex(ccTracks:Vector.<ClosedCaptionsTrack>,  
     ccTrackIndex:int):Number { 
       var count:Number = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in ccTracks) { 
           if (count < ccTrackIndex) 
               count = count + 1; 
           else 
               return count; 
       } 
       return -1; 
   } 
   
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks); 
   } 
   
   private function onCaptionUpdated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks,  
                     (_player.ccVisibility == MediaPlayer.VISIBLE) ?  
                      _player.currentItem.selectedClosedCaptionsTrack : null); 
   } 
   
   private function updateCCTracks(tracks:Vector.<ClosedCaptionsTrack>,  
     selectedTrack:ClosedCaptionsTrack = null):void { 
       _ccTracks.removeAll(); 
   
       _ccTracks.addItem( 
           { 
               "label": "CC off", 
               "data": "cc-off" 
           } 
       ); 
   
       var selectedIndex:int = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in tracks) { 
           _ccTracks.addItem( 
               { 
                   "label": ccTrack.name, 
                   "data": ccTrack.name 
               } 
           ); 
           if (selectedTrack && ccTrack.name == selectedTrack.name && 
           ccTrack.language == selectedTrack.language && 
           ccTrack.serviceType == selectedTrack.serviceType) { 
               selectedIndex = _ccTracks.length - 1; 
           } 
       } 
   
       var hasCC:Boolean = _ccTracks.length > 0; 
       ccTracksList.enabled = hasCC; 
       ccTracksList.mouseEnabled = hasCC; 
       ccTracksList.selectedIndex = selectedIndex; 
   } 
   ```

