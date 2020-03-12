---
description: Puede especificar varias opciones de estilo de rótulos y estas opciones anulan las opciones de estilo de los rótulos originales.
seo-description: Puede especificar varias opciones de estilo de rótulos y estas opciones anulan las opciones de estilo de los rótulos originales.
seo-title: Opciones de estilo de subtítulos opcionales
title: Opciones de estilo de subtítulos opcionales
uuid: 0e2fd9f3-e569-4b5d-9b78-86f8ee6230ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Opciones de estilo de subtítulos opcionales{#closed-caption-styling-options}

Puede especificar varias opciones de estilo de rótulos y estas opciones anulan las opciones de estilo de los rótulos originales.

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
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
   <td colname="2"> <p>Tipo de fuente. </p> <p>Solo se puede establecer en un valor definido por la enumeración <span class="codeph"> TextFormat.Font </span> y que represente, por ejemplo, un solo espacio con o sin serifs. </p> <p>Sugerencia:  Las fuentes disponibles en un dispositivo pueden variar y se utilizan sustituciones cuando es necesario. Monospace con serifs se utiliza generalmente como sustituto, aunque esta sustitución puede ser específica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamaño </td> 
   <td colname="2"> <p>Tamaño del rótulo. </p> <p> Solo se puede establecer en un valor definido por la enumeración <span class="codeph"> TextFormat.Size </span> : 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIO </span> - Tamaño estándar </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE </span> - Aproximadamente 30% mayor que medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUEÑO </span> - Aproximadamente un 30% menor que medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDETERMINADO </span> : el tamaño predeterminado del rótulo; igual que medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fuente </td> 
   <td colname="2"> <p>Color de fuente. </p> <p>Solo se puede establecer en un valor definido por la enumeración <span class="codeph"> TextFormat.Color </span> . </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fondo </td> 
   <td colname="2"> <p>Color de celda de carácter de fondo. </p> <p>Solo se puede establecer en valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de fuente </td> 
   <td colname="2"> <p>La opacidad del texto. </p> <p>Expresado como porcentaje de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY </span> para la fuente es 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Margen inferior </td> 
   <td colname="2"> <p>Distancia vertical desde la parte inferior de la ventana del rótulo para evitar rótulos. </p> <p>Se expresa como un porcentaje de la altura de la ventana del rótulo (por ejemplo, "20 %") o un número de píxeles (por ejemplo, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Área segura </td> 
   <td colname="2"> <p>Región alrededor del borde de la pantalla entre 0 % y 25 % en la que no aparecerán rótulos. </p> <p>De forma predeterminada, el área segura para 608/708 es 12% y el área segura para WebVTT es 0%. Esta configuración permite que la aplicación sobrescriba ese valor predeterminado. Si se proporcionan dos valores, por ejemplo, la cadena "10 %,20 %", el primer valor es el área segura horizontal y el segundo valor es el área segura vertical. Si se proporciona un valor, por ejemplo, la cadena "15%", los ejes vertical y horizontal utilizan el área segura especificada. </p> </td> 
  </tr> 
 </tbody> 
</table>

