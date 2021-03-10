---
title: Capacidades del dispositivo necesarias para reproducir contenido protegido
description: Capacidades del dispositivo necesarias para reproducir contenido protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Funcionalidades de dispositivo necesarias para reproducir contenido protegido {#device-capabilities-required-to-play-protected-content}

Especifica las capacidades de hardware necesarias para acceder al contenido. La información sobre las capacidades de hardware está disponible para los dispositivos que utilizan el kit de portado.

Las capacidades del dispositivo se pueden identificar mediante los atributos especificados en la siguiente tabla:

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Atributo</b> </td> 
   <td><b>Valores admitidos</b> </td> 
   <td><b>Criterios de coincidencia</b> </td> 
   <td><b>Descripción</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Bus accesible para no usuario </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Coincidencia exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si es true, el dispositivo no debe tener un bus accesible para el usuario. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Raíz de hardware de confianza </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Maqueta exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si es true, el dispositivo debe tener una raíz de hardware de confianza. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Esta regla de uso es compatible con los clientes de acceso a Adobe versión 2.0.2 y posteriores. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias. Consulte [Versión mínima del cliente](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).

