---
description: Puede proporcionar información de estilo para las pistas de subtítulos cerrados mediante la clase ClosedCaptionStyles. Esto establece el estilo de cualquier subtítulo que se muestre en el reproductor.
title: Control del estilo de subtítulos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Control del estilo de subtítulos{#control-closed-caption-styling}

Puede proporcionar información de estilo para las pistas de subtítulos cerrados mediante la clase ClosedCaptionStyles. Esto establece el estilo de cualquier subtítulo que se muestre en el reproductor.

Esta clase encapsula información de estilo de subtítulos, como el tipo de fuente, el tamaño, el color y la opacidad de fondo. Una clase de ayuda asociada, `ClosedCaptionStylesBuilder`, facilita el trabajo con la configuración de estilo de subtítulos.

## Definir estilos de subtítulos {#section_DAE84659D1964DB1B518F91B59AF29D9}

Puede aplicar estilo al texto de subtítulos opcionales con métodos TVSDK.

1. Espere a que MediaPlayer tenga al menos el estado PREPARADO (consulte [Esperar a un estado válido](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Para cambiar la configuración de estilo, realice una de las siguientes acciones:

   * Utilice el `ClosedCaptionStylesBuilder` clase auxiliar (funciona con `ClosedCaptionStyles` entre bastidores).
   * Utilice el `ClosedCaptionStyles` clase directamente.

>[!NOTE]
>
>La configuración del estilo de subtítulos es una operación asincrónica, por lo que los cambios pueden tardar unos segundos en aparecer en la pantalla.

## Opciones de estilo de subtítulos {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

Puede proporcionar información de estilo para pistas de subtítulos cerrados mediante el `ClosedCaptionStyles` clase. Esto establece el estilo de cualquier subtítulo que se muestre en el reproductor.

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
```

>[!TIP]
>
>En las opciones que definen los valores predeterminados (por ejemplo, `DEFAULT`), ese valor hace referencia a la configuración utilizada cuando se especificó originalmente el pie de ilustración.

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
   <td colname="2"> <p>El tipo de fuente. </p> <p>Solo se puede establecer en un valor definido por la variable <span class="codeph"> ClosedCaptionStyles.FONT </span> matriz y representa, por ejemplo, monoespaciado con o sin serifs. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>Sugerencia: Las fuentes reales disponibles en un dispositivo pueden variar y se utilizan sustituciones cuando es necesario. El monoespacio con serifs suele utilizarse como sustituto, aunque esta sustitución puede ser específica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamaño </td> 
   <td colname="2"> <p>El tamaño del pie de ilustración. </p> <p> Solo se puede establecer en un valor definido por la variable <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span> matriz: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIO </span> - La talla estándar </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE </span> - Aproximadamente un 30% más grande que el medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUEÑO </span> - Aproximadamente un 30% más pequeño que el medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDETERMINADO </span> : el tamaño predeterminado para el pie de ilustración; igual que el medio </li> 
     </ul> </p> <p>Sugerencia: Para cambiar el tamaño de fuente de los subtítulos WebVTT, cambie el parámetro de tamaño del <span class="codeph"> Establecedor de DefaultMediaPlayer.ccStyles </span> función. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Borde de fuente </td> 
   <td colname="2"> <p>Efecto utilizado para el borde de la fuente, como elevado o ninguno. </p> <p>Solo se puede establecer en un valor definido por la variable <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span> matriz. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fuente </td> 
   <td colname="2"> <p>El color de fuente. </p> <p>Solo se puede establecer en un valor definido por la variable <span class="codeph"> ClosedCaptionStyles.COLOR </span> matriz. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de borde </td> 
   <td colname="2"> <p>Color del efecto de borde. </p> <p>Se puede establecer en cualquiera de los valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fondo </td> 
   <td colname="2"> <p>Color de la celda de caracteres de fondo. </p> <p>Solo se puede establecer en valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de relleno </td> 
   <td colname="2"> <p>Color del fondo de la ventana en la que se encuentra el texto. </p> <p>Se puede establecer en cualquiera de los valores disponibles para el color de fuente. </p> <p>Importante: Esto no se aplica a los subtítulos WebVTT, ya que WebVTT no utiliza esta función. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de fuente </td> 
   <td colname="2"> <p>Opacidad del texto. </p> <p>Expresado como porcentaje de 0 (completamente transparente) a 100 (completamente opaco). <span class="codeph"> OPACIDAD_PREDETERMINADA </span> para la fuente es 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de fondo </td> 
   <td colname="2"> <p>Opacidad de la celda de caracteres de fondo. </p> <p>Expresado como porcentaje de 0 (completamente transparente) a 100 (completamente opaco). <span class="codeph"> OPACIDAD_PREDETERMINADA </span> para el fondo es 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de relleno </td> 
   <td colname="2"> <p>Opacidad del fondo de la ventana de rótulo. </p> <p>Expresado como porcentaje de 0 (completamente transparente) a 100 (completamente opaco). <span class="codeph"> OPACIDAD_PREDETERMINADA </span> para el relleno es 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Ejemplos: Caption formatting {#section_63E33840B7A14D26990046E2ACF2ECA1}

Puede especificar el formato de subtítulos.

## Ejemplo 1: Especificar valores de formato explícitamente {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## Ejemplo 2: Especificar valores de formato en parámetros {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
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
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
