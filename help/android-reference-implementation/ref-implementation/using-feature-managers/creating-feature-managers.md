---
description: Las funciones de TVSDK se rigen por la configuración y se implementan mediante MediaPlayer.
seo-description: Las funciones de TVSDK se rigen por la configuración y se implementan mediante MediaPlayer.
seo-title: Creación de administradores de funciones pasando la información de configuración a MediaPlayer
title: Creación de administradores de funciones pasando la información de configuración a MediaPlayer
uuid: 106ececd-a670-4360-b000-a31fec65233c
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Creación de administradores de funciones pasando la información de configuración a MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Las funciones de TVSDK se rigen por la configuración y se implementan mediante MediaPlayer.

* La configuración es la lista de opciones específicas para la función, como la velocidad de bits inicial del control ABR y la visibilidad de subtítulos opcionales predeterminada.

   Los administradores de funciones necesitan obtener las configuraciones para determinar el comportamiento de la función.

   En la implementación de referencia de Primetime, la configuración se almacena en las preferencias compartidas, pero puede almacenar la configuración de cualquier manera que sea conveniente para su entorno.

* `MediaPlayer` es el objeto del reproductor de medios TVSDK que contiene el recurso de vídeo.

   Los administradores de funciones registran los oyentes de evento TVSDK en este objeto de reproductor, recuperan datos de la sesión de reproducción y activan las funciones de TVSDK en la sesión de reproducción.

Cada función tiene una interfaz de configuración correspondiente. Por ejemplo, `CCManager` utiliza `ICCConfig` para recuperar la configuración. `ICCConfig` contiene métodos para obtener la información de configuración relacionada solo con subtítulos opcionales.

El siguiente ejemplo muestra el archivo [!DNL ICCConfig.java], configurado para recibir información sobre la visibilidad de subtítulos opcionales, el estilo de fuente y el borde de fuente de `MediaPlayer`:

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

Una aplicación que utiliza una función TVSDK puede crear su administrador de funciones con un proveedor de configuración y un objeto `MediaPlayer`. Por ejemplo:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

Documentos de API de configuración del administrador de funciones: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)