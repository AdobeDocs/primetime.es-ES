---
title: Seguridad de capa de red
description: Seguridad de capa de red
copied-description: true
exl-id: 70c9917d-32bc-43f6-add3-62883f98ac5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Seguridad de capa de red{#network-layer-security}

Las vulnerabilidades de seguridad de red están entre las principales amenazas a las que está expuesto un servidor de aplicaciones orientado a Internet o a la intranet. En esta sección se describe el proceso de protección de los hosts de la red frente a estas vulnerabilidades. Aborda la segmentación de red, la protección de pila del Protocolo de control de transmisión/Protocolo Internet (TCP/IP) y el uso de cortafuegos para la protección del host.

Esta tabla describe técnicas comunes que reducen las vulnerabilidades de seguridad de red.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Técnica </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Zonas desmilitarizadas (DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentación debe existir en al menos dos niveles con el servidor de aplicaciones utilizado para ejecutar el acceso de Adobe detrás del cortafuegos interno. Separe la red externa de la DMZ que contiene los servidores web, que a su vez deben separarse de la red interna. Utilice cortafuegos para implementar las capas de separación. Categorice y controle el tráfico que pasa por cada capa de red para asegurarse de que solo se permite el mínimo absoluto de datos requerido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Direcciones IP privadas </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice la traducción de direcciones de red (NAT) con direcciones IP privadas (RFC 1918) en servidores de aplicaciones de acceso a Adobe. Asigne direcciones IP privadas (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) para que sea más difícil para un atacante enrutar el tráfico hacia y desde un host interno NAT a través de Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Cortafuegos </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice los siguientes criterios para seleccionar una solución de cortafuegos: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implemente servidores de seguridad que admitan servidores proxy o inspección de estado en lugar de soluciones simples de filtrado de paquetes. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Utilice un cortafuegos compatible con un paradigma de seguridad en el que pueda denegar todos los servicios excepto los explícitamente permitidos. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implemente una solución de cortafuegos de doble alojamiento o multialojamiento. Esta arquitectura proporciona el bueno nivel de seguridad y ayuda a evitar que usuarios no autorizados eludan la seguridad del cortafuegos. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
