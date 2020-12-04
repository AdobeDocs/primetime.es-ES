---
description: Puede proporcionar información de estilo para las pistas de subtítulos opcionales mediante la clase TextFormat, que establece el estilo de los subtítulos cerrados que muestra el reproductor.
seo-description: Puede proporcionar información de estilo para las pistas de subtítulos opcionales mediante la clase TextFormat, que establece el estilo de los subtítulos cerrados que muestra el reproductor.
seo-title: Control del estilo de los subtítulos opcionales
title: Control del estilo de los subtítulos opcionales
uuid: fa4f637f-f13c-465d-8eee-5e66a6dd9db2
translation-type: tm+mt
source-git-commit: b02dfafdc78ca209da5ba0ed855342952be4288f
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---


# Control del estilo de subtítulos optativos {#control-closed-caption-styling}

Puede proporcionar información de estilo para las pistas de subtítulos opcionales mediante la clase TextFormat, que establece el estilo de los subtítulos cerrados que muestra el reproductor.

Esta clase encapsula información de estilo de subtítulos opcionales, como el tipo de fuente, el tamaño, el color y la opacidad de fondo.

## Establecer estilos de subtítulos opcionales {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

Puede aplicar estilo al texto de subtítulos opcionales con métodos TVSDK.

1. Espere a que el reproductor de medios esté al menos en el estado `PREPARED`.
1. Cree una instancia `TextFormatBuilder`.

   Puede proporcionar todos los parámetros de estilo de subtítulos opcionales ahora o establecerlos más tarde.

   TVSDK encapsula información de estilo de subtítulos opcionales en la interfaz `TextFormat`. La clase `TextFormatBuilder` crea objetos que implementan esta interfaz.

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. Para obtener una referencia a un objeto que implementa la interfaz `TextFormat`, llame al método público `TextFormatBuilder.toTextFormat`.

   >[!NOTE]
   >
   >Esto devuelve un objeto `TextFormat` que se puede aplicar al reproductor de medios.

   ```java
   public TextFormat toTextFormat()
   ```

1. Opcionalmente, obtenga la configuración actual del estilo de subtítulos opcionales realizando una de las siguientes acciones:

   * Obtenga todos los ajustes de estilo con `MediaPlayer.getCCStyle` El valor devuelto es una instancia de la interfaz `TextFormat`.

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * Obtenga la configuración de uno en uno a través de los métodos de captador de la interfaz `TextFormat`.

      ```java
      public java.lang.String getFontColor(); 
      public java.lang.String getBackgroundColor(); 
      public java.lang.String getFillColor(); // retrieve the font fill color 
      public java.lang.String getEdgeColor(); // retrieve the font edge color 
      public TextFormat.Size getSize(); // retrieve the font size 
      public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
      public TextFormat.Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity(); 
      public java.lang.String getBottomInset(java.lang.String bi); 
      public java.lang.String getSafeArea(java.lang.String sa);
      ```

1. Para cambiar la configuración de estilo, realice una de las siguientes acciones:

   * Utilice el método setter `MediaPlayer.setCCStyle`, pasando una instancia de la interfaz `TextFormat`:

      ```java
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws MediaPlayerException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
      ```

   * Utilice la clase `TextFormatBuilder`, que define métodos de establecedor individuales.

      La interfaz `TextFormat` define un objeto inmutable, por lo que solo hay métodos de captador y no hay definidores. Los parámetros de estilo de subtítulos opcionales solo se pueden definir con la clase `TextFormatBuilder`:

      ```java
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(String backgroundColor) 
      public void setFillColor(String fillColor) 
      // set the font-edge color 
      public void setEdgeColor(String edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(String fontColor) 
      public void setBottomInset(String bi) 
      public void setSafeArea(String sa) 
      public void setTreatSpaceAsAlphaNum(bool)
      ```

      >[!IMPORTANT]
      >
      >**Configuración de color:** en Android TVSDK 2.X, se ha mejorado el estilo de color de los subtítulos opcionales. La mejora permite definir colores de subtítulos cerrados mediante una cadena hexadecimal que representa valores de color RGB. La representación de color RGB hexadecimal es la cadena de 6 bytes que se utiliza en aplicaciones como Photoshop:
      >
      >* FFFFFF = negro
      >* 000000 = Blanco
      >* FF0000 = Rojo
      >* 00FF00 = Verde
      >* 0000FF = Azul

      >
      >y así sucesivamente.
      >
      >En la aplicación, siempre que pase información de estilo de color a `TextFormatBuilder`, seguirá utilizando la lista desglosada `Color` como antes, pero ahora debe agregar `getValue()` al color para obtener el valor como una cadena. Por ejemplo:
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```




La configuración del estilo de subtítulos opcionales es una operación asincrónica, por lo que los cambios pueden tardar hasta unos segundos en aparecer en la pantalla.

## Opciones de estilo de subtítulos opcionales {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

Puede especificar varias opciones de estilo de rótulos y estas opciones anulan las opciones de estilo de los rótulos originales.

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
```

>[!TIP]
>
>En las opciones que definen los valores predeterminados (por ejemplo, `DEFAULT`), ese valor hace referencia a la configuración cuando se especificó originalmente el rótulo.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Formato </th> 
   <th colname="2" class="entry"> Descripción </th> 
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
  <tr rowsep="1"> 
   <td colname="1"> Margen inferior </td> 
   <td colname="2"> <p>Distancia vertical desde la parte inferior de la ventana del rótulo para evitar rótulos. </p> <p>Se expresa como un porcentaje de la altura de la ventana del rótulo (por ejemplo, "20 %") o un número de píxeles (por ejemplo, "20"). </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Área segura </td> 
   <td colname="2"> <p>Región alrededor del borde de la pantalla entre 0 % y 25 % en la que no aparecerán rótulos. </p> <p>De forma predeterminada, el área segura para WebVTT es 0%. Esta configuración permite que la aplicación sobrescriba ese valor predeterminado. Si se proporcionan dos valores, por ejemplo, la cadena "10 %,20 %", el primer valor es el área segura horizontal y el segundo valor es el área segura vertical. Si se proporciona un valor, por ejemplo, la cadena "15%", los ejes vertical y horizontal utilizan el área segura especificada. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Ejemplos de formato de rótulo {#section_58E8E82494EC4683B010FFDE67485CF9}

Estos son algunos ejemplos que muestran cómo especificar el formato de los subtítulos opcionales.

**Ejemplo 1: Especificar valores de formato explícitamente**

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
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
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
