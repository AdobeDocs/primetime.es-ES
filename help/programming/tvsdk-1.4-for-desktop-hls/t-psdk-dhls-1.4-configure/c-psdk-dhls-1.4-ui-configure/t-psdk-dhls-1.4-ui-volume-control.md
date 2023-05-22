---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
exl-id: 058d79d2-35cc-4238-8fc1-2820a2d91ffb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia de MediaPlayer esté en un estado válido para este comando.

   Cualquier estado excepto RELEASED es válido.
1. Llame al método del conjunto de volúmenes en el `MediaPlayer` para configurar el volumen de audio.

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
      <td colname="col1"> Bueno que 1 </td> 
      <td colname="col2"> El valor dividido entre 100 y establecido en uno de los siguientes valores: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">El resultado si está entre 0 y 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 si el resultado es bueno que 1 </li> 
      </ul> <p>Sugerencia: Esta lógica gestiona los valores proporcionados por los clientes en función de versiones anteriores de 
      <span class="codeph">frases/primetime-sdk-name</span>, donde los valores de volumen oscilaron entre 0 y 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
