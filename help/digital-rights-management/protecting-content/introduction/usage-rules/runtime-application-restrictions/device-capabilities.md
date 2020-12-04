---
description: 'null'
seo-description: 'null'
seo-title: Funciones de dispositivo necesarias para reproducir contenido protegido
title: Funciones de dispositivo necesarias para reproducir contenido protegido
uuid: 1490711b-65d9-4716-8779-ae1da7d2c82c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Capacidades del dispositivo requeridas para reproducir contenido protegido {#device-capabilities-required-to-play-protected-content}

Las capacidades del dispositivo requeridas especifican las capacidades de hardware necesarias para acceder al contenido. La información sobre las capacidades de hardware está disponible para dispositivos que utilizan el kit de portación.

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Bus accesible para usuarios no usuarios </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Coincidencia exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si es true, el dispositivo no debe tener un bus accesible para el usuario. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Raíz de hardware de confianza </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Coincidencia exacta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Si es true, el dispositivo debe tener una raíz de hardware de confianza. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Esta regla de uso es compatible con los clientes de Adobe Primetime DRM versión 2.0.2 y posterior. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias.
>
>Consulte [Versión mínima del cliente](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).

