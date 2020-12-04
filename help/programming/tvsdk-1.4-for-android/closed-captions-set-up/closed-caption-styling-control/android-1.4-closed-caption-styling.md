---
description: Puede proporcionar información de estilo para las pistas de subtítulos opcionales mediante la clase TextFormat. Esto establece el estilo de cualquier subtítulo cerrado que muestre el reproductor.
seo-description: Puede proporcionar información de estilo para las pistas de subtítulos opcionales mediante la clase TextFormat. Esto establece el estilo de cualquier subtítulo cerrado que muestre el reproductor.
seo-title: Control del estilo de los subtítulos opcionales
title: Control del estilo de los subtítulos opcionales
uuid: 331b0833-3e8a-482e-a3df-5e92b69d0a94
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---


# Control del estilo de subtítulos optativos {#control-closed-caption-styling-overview}

Puede proporcionar información de estilo para las pistas de subtítulos opcionales mediante la clase TextFormat. Esto establece el estilo de cualquier subtítulo cerrado que muestre el reproductor.

Esta clase encapsula información de estilo de subtítulos opcionales, como el tipo de fuente, el tamaño, el color y la opacidad de fondo. Una clase auxiliar asociada, `TextFormatBuilder`, facilita el trabajo con la configuración de estilo de subtítulos opcionales.

## Establecer estilos de subtítulos opcionales {#set-closed-caption-styles}

Puede aplicar estilo al texto de subtítulos opcionales con métodos TVSDK.

1. Espere a que el reproductor de medios esté al menos en el estado PREPARADO.
1. Cree una instancia `TextFormatBuilder`.

   Puede proporcionar todos los parámetros de estilo de subtítulos opcionales ahora o establecerlos más tarde.

   TVSDK encapsula información de estilo de subtítulos opcionales en la interfaz `TextFormat`. La clase `TextFormatBuilder` crea objetos que implementan esta interfaz.

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. Para obtener una referencia a un objeto que implementa la interfaz `TextFormat`, llame al método público `TextFormatBuilder.toTextFormat`.

   Esto devuelve un objeto `TextFormat` que se puede aplicar al reproductor de medios.

   ```java
   public TextFormat toTextFormat()
   ```

1. Opcionalmente, obtenga la configuración actual del estilo de subtítulos opcionales realizando una de las siguientes acciones:

   * Obtenga todos los ajustes de estilo con `MediaPlayer.getCCStyle`.

      El valor devuelto es una instancia de la interfaz `TextFormat`.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * Obtenga la configuración de uno en uno a través de los métodos de captador de la interfaz `TextFormat`.

      ```js
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. Para cambiar la configuración de estilo, realice una de las siguientes acciones:

   >[!NOTE]
   >
   >No puede cambiar el tamaño de los subtítulos WebVTT.

   * Utilice el método setter `MediaPlayer.setCCStyle`, pasando una instancia de la interfaz `TextFormat`:

      ```js
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

   * Utilice la clase `TextFormatBuilder`, que define métodos de establecedor individuales.

      La interfaz `TextFormat` define un objeto inmutable, por lo que solo hay métodos de captador y no hay definidores. Los parámetros de estilo de subtítulos opcionales solo se pueden definir con la clase `TextFormatBuilder`:

      ```js
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

La configuración del estilo de subtítulos opcionales es una operación asincrónica, por lo que los cambios pueden tardar hasta unos segundos en aparecer en la pantalla.

## Opciones de estilo de subtítulos opcionales {#closed-caption-styling-options}

Puede especificar varias opciones de estilo de rótulos y estas opciones anulan las opciones de estilo de los rótulos originales

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>En las opciones que definen los valores predeterminados (por ejemplo, PREDETERMINADO), ese valor hace referencia a la configuración que tenía cuando se especificó originalmente el rótulo.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Formato </b></th> 
   <th colname="2" class="entry"> <b>Descripción</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Fuente </td> 
   <td colname="2"> <p>Tipo de fuente. </p> <p>Sólo se puede establecer en un valor definido por la lista desglosada <span class="codeph"> TextFormat.Font </span> y que represente, por ejemplo, un solo espacio con o sin serifs. </p> <p>Sugerencia:  Las fuentes disponibles en un dispositivo pueden variar y se utilizan sustituciones cuando es necesario. Monospace con serifs se utiliza generalmente como sustituto, aunque esta sustitución puede ser específica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamaño </td> 
   <td colname="2"> <p>Tamaño del rótulo. </p> <p> Sólo se puede establecer en un valor definido por la lista desglosada <span class="codeph"> TextFormat.Size </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIO  </span> - Tamaño estándar </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE  </span> - Aproximadamente 30% mayor que medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUEÑO  </span> - Aproximadamente un 30% menor que medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDETERMINADO  </span> - El tamaño predeterminado del rótulo; igual que medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Borde de fuente </td> 
   <td colname="2"> <p>Efecto utilizado para el borde de la fuente, como elevado o ninguno. </p> <p>Solo se puede establecer en un valor definido por la lista desglosada <span class="codeph"> TextFormat.FontEdge </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fuente </td> 
   <td colname="2"> <p>Color de fuente. </p> <p>Sólo se puede establecer en un valor definido por la lista desglosada <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de borde </td> 
   <td colname="2"> <p>Color del efecto de borde. </p> <p>Se puede establecer en cualquiera de los valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fondo </td> 
   <td colname="2"> <p>Color de celda de carácter de fondo. </p> <p>Solo se puede establecer en valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de relleno </td> 
   <td colname="2"> <p>Color del fondo de la ventana en la que se encuentra el texto. </p> <p>Se puede establecer en cualquiera de los valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de fuente </td> 
   <td colname="2"> <p>La opacidad del texto. </p> <p>Expresado como porcentaje de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para la fuente es 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad del fondo </td> 
   <td colname="2"> <p>La opacidad de la celda de caracteres de fondo. </p> <p>Expresado como porcentaje de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para el fondo es 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de relleno </td> 
   <td colname="2"> <p>La opacidad del fondo de la ventana de rótulo. </p> <p>Expresado como porcentaje de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para relleno es 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Ejemplos de formato de rótulo {#examples-caption-formatting}

Puede especificar el formato de los subtítulos opcionales.

**Ejemplo 1: Especificar valores de formato explícitamente**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**Ejemplo 2: Especificar valores de formato en parámetros**

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity  
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity.  
*/ 
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
