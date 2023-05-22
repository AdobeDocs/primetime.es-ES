---
title: Funciones del dispositivo necesarias para reproducir contenido protegido
description: Funciones del dispositivo necesarias para reproducir contenido protegido
copied-description: true
exl-id: 540fbb53-ec1a-43be-b51b-9937ed31e384
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Funciones del dispositivo necesarias para reproducir contenido protegido {#device-capabilities-required-to-play-protected-content}

Las funcionalidades de dispositivo requeridas especifican las funcionalidades de hardware necesarias para acceder al contenido. La información acerca de las funciones de hardware está disponible para los dispositivos que utilizan el kit de portabilidad.

Los atributos siguientes pueden identificar las capacidades del dispositivo:

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
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si el valor es True, el dispositivo no debe tener un bus accesible para el usuario. </p> </td> 
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
>Esta regla de uso es compatible con los clientes DRM de Adobe Primetime versión 2.0.2 y posteriores. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente que admita el servidor de licencias.
>
>Consulte [Versión mínima del cliente](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
