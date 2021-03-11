---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia de MediaPlayer esté en un estado válido para este comando.

   Cualquier estado que no sea LANZADO es válido.
1. Llame al método del conjunto de volúmenes en la instancia `MediaPlayer` para configurar el volumen de audio.

   ```
   public function set volume(value:Number):void
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 no dice nada y 1 es el volumen máximo.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Si el volumen especificado es </th> 
      <th colname="col2" class="entry"> El volumen resultante es </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Menor que 0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Entre 0 y 1 </td> 
      <td colname="col2"> El volumen especificado </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Bueno a 1 </td> 
      <td colname="col2"> El valor se divide entre 100 y se establece en uno de los siguientes valores: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">El resultado si está entre 0 y 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 si el resultado es bueno a 1 </li> 
      </ul> <p>Sugerencia:  Esta lógica gestiona los valores que proporcionan los clientes en función de versiones anteriores de 
      <span class="codeph">frases/primetime-sdk-name</span>, donde los valores de volumen oscilaban entre 0 y 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
