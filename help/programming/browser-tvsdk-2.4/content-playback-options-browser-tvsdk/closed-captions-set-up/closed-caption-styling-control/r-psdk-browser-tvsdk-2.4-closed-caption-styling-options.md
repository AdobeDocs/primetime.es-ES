---
description: Puede especificar varias opciones de estilo de rótulo, y estas opciones anulan las opciones de estilo de los rótulos originales.
title: Opciones de estilo de subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Opciones de estilo de subtítulos{#closed-caption-styling-options}

Puede especificar varias opciones de estilo de rótulo, y estas opciones anulan las opciones de estilo de los rótulos originales.

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
   <td colname="2"> <p>Tipo de fuente. </p> <p>Solo se puede establecer en un valor que esté definido por la enumeración <span class="codeph"> TextFormat.Font </span> y que represente, por ejemplo, espaciado con o sin serifs. </p> <p>Sugerencia:  Las fuentes disponibles en un dispositivo pueden variar y se utilizan sustituciones cuando es necesario. Monospace con serifs se suele utilizar como sustituto, aunque esta sustitución puede ser específica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamaño </td> 
   <td colname="2"> <p>El tamaño del rótulo. </p> <p> Solo se puede establecer en un valor definido por la enumeración <span class="codeph"> TextFormat.Size </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIO  </span> - Tamaño estándar </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE  </span> - Aproximadamente un 30% mayor que medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUEÑO  </span> - Aproximadamente un 30% menor que medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDETERMINADO:  </span> el tamaño predeterminado del rótulo; igual que medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fuente </td> 
   <td colname="2"> <p>El color de la fuente. </p> <p>Solo se puede establecer en un valor definido por la enumeración <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Color de fondo </td> 
   <td colname="2"> <p>El color de la celda del carácter de fondo. </p> <p>Solo se puede establecer en valores disponibles para el color de fuente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidad de fuente </td> 
   <td colname="2"> <p>La opacidad del texto. </p> <p>Se expresa como porcentaje de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para la fuente es 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Incrustación inferior </td> 
   <td colname="2"> <p>Distancia vertical desde la parte inferior de la ventana del rótulo para evitar rótulos. </p> <p>Se expresa como un porcentaje de la altura de la ventana del rótulo (por ejemplo, "20 %") o un número de píxeles (por ejemplo, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Área segura </td> 
   <td colname="2"> <p>Región alrededor del borde de la pantalla entre 0% y 25%, donde no aparecerán subtítulos. </p> <p>De forma predeterminada, el área segura para 608/708 es del 12% y el área segura para WebVTT es del 0%. Esta configuración permite que la aplicación anule esa opción predeterminada. Si se proporcionan dos valores, por ejemplo, la cadena "10%,20%", el primer valor es el área segura horizontal y el segundo valor es el área segura vertical. Si se proporciona un valor, por ejemplo, la cadena "15%", los ejes vertical y horizontal utilizan el área segura especificada. </p> </td> 
  </tr> 
 </tbody> 
</table>

