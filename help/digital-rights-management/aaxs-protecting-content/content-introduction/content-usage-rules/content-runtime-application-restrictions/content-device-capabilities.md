---
title: Funciones del dispositivo necesarias para reproducir contenido protegido
description: Funciones del dispositivo necesarias para reproducir contenido protegido
copied-description: true
exl-id: 5f2089e9-3176-46a7-9998-2dad0e77e453
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Funciones del dispositivo necesarias para reproducir contenido protegido {#device-capabilities-required-to-play-protected-content}

Especifica las funciones de hardware necesarias para acceder al contenido. La información acerca de las funciones de hardware está disponible para los dispositivos que utilizan el kit de portabilidad.

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Bus no accesible para el usuario </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Coincidencia exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si el valor es True, el dispositivo no debe tener un bus accesible al usuario. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Raíz de confianza de hardware </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Coincidencia exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si el valor es True, el dispositivo debe tener una raíz de hardware de confianza. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Esta regla de uso es compatible con la versión 2.0.2 y posteriores de los clientes de Adobe Access. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente que admita el servidor de licencias. Consulte. [Versión mínima del cliente](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).
