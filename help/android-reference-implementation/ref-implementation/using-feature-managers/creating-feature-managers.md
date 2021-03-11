---
description: Las funciones de TVSDK se rigen por la configuración y se implementan mediante MediaPlayer.
title: Creación de administradores de funciones pasando información de configuración a MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Creación de administradores de funciones pasando información de configuración a MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Las funciones de TVSDK se rigen por la configuración y se implementan mediante MediaPlayer.

* La configuración es la lista de configuraciones específicas para la función, como la velocidad de bits inicial del control ABR y la visibilidad de los subtítulos predeterminados.

   Los administradores de funciones deben obtener las configuraciones para determinar el comportamiento de las funciones.

   En la implementación de referencia de Primetime, la configuración se almacena en las preferencias compartidas, pero puede almacenar la configuración de cualquier manera que sea apropiada para su entorno.

* `MediaPlayer` es el objeto de reproductor de medios TVSDK que contiene el recurso de vídeo.

   Los administradores de funciones registran los oyentes de eventos TVSDK en este objeto de reproductor, recuperan los datos de la sesión de reproducción y las funciones TVSDK de déclencheur en la sesión de reproducción.

Cada función tiene una interfaz de configuración correspondiente. Por ejemplo, `CCManager` utiliza `ICCConfig` para recuperar la configuración. `ICCConfig` contiene métodos para obtener la información de configuración relacionada únicamente con los subtítulos.

El siguiente ejemplo muestra el archivo [!DNL ICCConfig.java], configurado para recibir información sobre la visibilidad de los subtítulos cerrados, el estilo de fuente y el borde de fuente de `MediaPlayer`:

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