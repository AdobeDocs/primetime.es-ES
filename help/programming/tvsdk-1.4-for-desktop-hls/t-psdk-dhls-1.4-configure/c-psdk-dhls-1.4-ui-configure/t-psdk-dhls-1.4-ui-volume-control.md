---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
seo-description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
seo-title: Proporcionar control de volumen
title: Proporcionar control de volumen
uuid: c51e99b6-efd1-414e-9ef7-77bd53e0d6c0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia de MediaPlayer tenga un estado válido para este comando.

   Cualquier estado excepto RELEASED es válido.
1. Llame al método de conjunto de volúmenes en la instancia `MediaPlayer` para establecer el volumen de audio.

   ```
   public function set volume(value:Number):void
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 es silencioso y 1 es el volumen máximo.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Si el volumen especificado es </th> 
      <th colname="col2" class="entry"> El volumen resultante es </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Menos de 0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Entre 0 y 1 </td> 
      <td colname="col2"> El volumen especificado </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Bueno de 1 </td> 
      <td colname="col2"> El valor dividido por 100 y establecido en uno de los siguientes valores: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">El resultado si está entre 0 y 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 si el resultado es bueno a 1 </li> 
      </ul> <p>Sugerencia:  Esta lógica gestiona los valores suministrados por los clientes en función de versiones anteriores de 
      <span class="codeph">frases/primetime-sdk-name</span>, donde los valores de volumen oscilaban entre 0 y 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
