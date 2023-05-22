---
description: Debe separar la lógica de la interfaz de usuario del reproductor del proceso que administra los clics en los anuncios. Una forma de hacerlo es implementar varios fragmentos para una actividad.
title: Separar el proceso de publicidad en el que se puede hacer clic
exl-id: 6519b8ed-2963-4708-bbb9-8ff178c1fa86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Separar el proceso de publicidad en el que se puede hacer clic{#separate-the-clickable-ad-process}

Debe separar la lógica de la interfaz de usuario del reproductor del proceso que administra los clics en los anuncios. Una forma de hacerlo es implementar varios fragmentos para una actividad.

1. Implementar un fragmento para contener el `MediaPlayer` y que será responsable de la reproducción del vídeo.

   Este fragmento debería llamar a `notifyClick`.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. Implemente un fragmento diferente para mostrar un elemento de la interfaz de usuario que indique que se puede hacer clic en un anuncio, supervise ese elemento de la interfaz de usuario y comunique los clics del usuario al fragmento que contiene el fragmento `MediaPlayer`.

   Este fragmento debe declarar una interfaz para la comunicación con el fragmento. El fragmento captura la implementación de la interfaz durante su método de ciclo vital onAttach y puede llamar a los métodos de interfaz para comunicarse con Activity Map.

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
