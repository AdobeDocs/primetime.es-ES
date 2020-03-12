---
seo-title: Funciones de dispositivo necesarias para reproducir contenido protegido
title: Funciones de dispositivo necesarias para reproducir contenido protegido
uuid: 16ed73d9-e02f-4c86-bf15-2d3e7122bf5a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Funciones de dispositivo necesarias para reproducir contenido protegido {#device-capabilities-required-to-play-protected-content}

Especifica las capacidades de hardware necesarias para acceder al contenido. La información sobre las capacidades de hardware está disponible para dispositivos que utilizan el kit de portación.

Las capacidades del dispositivo pueden identificarse mediante los atributos especificados en la siguiente tabla:

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Atributo</b> </td> 
   <td><b>Valores admitidos</b> </td> 
   <td><b>Criterios de coincidencia</b> </td> 
   <td><b>Descripción</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Bus accesible para usuarios no usuarios </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Coincidencia exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si es true, el dispositivo no debe tener un bus accesible para el usuario. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Raíz de hardware de confianza </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Máscara exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si es true, el dispositivo debe tener una raíz de hardware de confianza. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Esta regla de uso es compatible con los clientes de Adobe Access versión 2.0.2 y posterior. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias. Consulte Versión [mínima del cliente](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).

