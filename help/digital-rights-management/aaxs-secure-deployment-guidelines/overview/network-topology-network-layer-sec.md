---
seo-title: Seguridad de capa de red
title: Seguridad de capa de red
uuid: bd53bccf-1130-4189-97ec-4259bd25762f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Seguridad de capa de red{#network-layer-security}

Las vulnerabilidades de seguridad de red están entre las primeras amenazas para cualquier servidor de aplicaciones orientado a Internet o a intranet. Esta sección describe el proceso de endurecimiento de los hosts de la red contra estas vulnerabilidades. Se ocupa de la segmentación de red, el endurecimiento de la pila del Protocolo de control de transmisión/Protocolo de Internet (TCP/IP) y el uso de firewalls para la protección del host.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentación debe existir en al menos dos niveles con el servidor de aplicaciones utilizado para ejecutar Adobe Access situado detrás del servidor de seguridad interior. Separe la red externa de la DMZ que contiene los servidores Web, que a su vez deben separarse de la red interna. Utilice los cortafuegos para implementar las capas de separación. Clasifique y controle el tráfico que pasa por cada capa de red para asegurarse de que sólo se permite el mínimo absoluto de datos requeridos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Direcciones IP privadas </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice Traducción de direcciones de red (NAT) con direcciones IP privadas RFC 1918 en los servidores de aplicaciones de Adobe Access. Asigne direcciones IP privadas (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) para que sea más difícil para un atacante enrutar el tráfico hacia y desde un host interno NAT a través de Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Servidores de seguridad </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice los siguientes criterios para seleccionar una solución de firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implemente servidores de seguridad que admitan servidores proxy y/o inspecciones de estado en lugar de soluciones sencillas de filtrado de paquetes. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Utilice un servidor de seguridad que admita un paradigma de seguridad en el que puede denegar todos los servicios excepto los que se permiten explícitamente. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implemente una solución de cortafuegos que tenga dos o varios hogares. Esta arquitectura proporciona el nivel bueno de seguridad y ayuda a evitar que usuarios no autorizados pasen por alto la seguridad del cortafuegos. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

