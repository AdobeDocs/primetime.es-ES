---
description: Debe separar la lógica de IU del reproductor del proceso que administra los clics en publicidad. Una forma de hacerlo es implementar varios fragmentos para una Actividad.
seo-description: Debe separar la lógica de IU del reproductor del proceso que administra los clics en publicidad. Una forma de hacerlo es implementar varios fragmentos para una Actividad.
seo-title: Separe el proceso de publicidad en el que se puede hacer clic
title: Separe el proceso de publicidad en el que se puede hacer clic
uuid: 00537191-8997-418d-add2-8e86d818c76e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Separe el proceso de publicidad en el que se puede hacer clic{#separate-the-clickable-ad-process}

Debe separar la lógica de IU del reproductor del proceso que administra los clics en publicidad. Una forma de hacerlo es implementar varios fragmentos para una Actividad.

1. Implemente un fragmento para contener `MediaPlayer` y que será responsable de la reproducción de vídeo.

   Este fragmento debe llamar a `notifyClick`.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implemente un fragmento diferente para mostrar un elemento de la interfaz de usuario que indique que se puede hacer clic en una publicidad, supervise ese elemento de la interfaz de usuario y comunique los clics del usuario al fragmento que contiene el `MediaPlayer`.

   Este fragmento debe declarar una interfaz para la comunicación de fragmentos. El fragmento captura la implementación de la interfaz durante su método de ciclo de vida onAttach y puede llamar a los métodos de interfaz para comunicarse con la Actividad.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
   
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container, Bundle 
                                savedInstanceState) { 
   
           // the custom fragment is defined by a custom button 
           viewGroup =  
             (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad, container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
   
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);  
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
               + " must implement OnAdUserInteraction"); 
           }  
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```

