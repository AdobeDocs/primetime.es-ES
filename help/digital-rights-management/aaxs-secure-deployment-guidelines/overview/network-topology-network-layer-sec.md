---
title: Seguridad de capa de red
description: Seguridad de capa de red
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Seguridad de capa de red{#network-layer-security}

Las vulnerabilidades de seguridad de red están entre las primeras amenazas para cualquier servidor de aplicaciones orientado a Internet o a la intranet. En esta sección se describe el proceso de endurecimiento de los hosts de la red contra estas vulnerabilidades. Se ocupa de la segmentación de red, el refuerzo de la pila del Protocolo de control de transmisión/Protocolo Internet (TCP/IP) y el uso de cortafuegos para la protección del host.

En esta tabla se describen técnicas comunes que reducen las vulnerabilidades de seguridad de la red.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentación debe existir en al menos dos niveles con el servidor de aplicaciones utilizado para ejecutar el acceso al Adobe colocado detrás del cortafuegos interno. Separe la red externa de la DMZ que contiene los servidores web, que a su vez deben separarse de la red interna. Utilice cortafuegos para implementar las capas de separación. Categorice y controle el tráfico que pasa por cada capa de red para garantizar que solo se permita el mínimo absoluto de datos requeridos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Direcciones IP privadas </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice Traducción de direcciones de red (NAT) con direcciones IP privadas RFC 1918 en servidores de aplicaciones de acceso a Adobe. Asigne direcciones IP privadas (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) para que sea más difícil para un atacante enrutar el tráfico hacia y desde un host interno NAT a través de Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice los siguientes criterios para seleccionar una solución de cortafuegos: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implemente firewalls que admitan servidores proxy o inspección de estado en lugar de soluciones sencillas de filtrado de paquetes. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Utilice un cortafuegos que admita un paradigma de seguridad en el que puede denegar todos los servicios, excepto los que estén explícitamente permitidos. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implemente una solución de firewall que tenga dos hogares o varios hogares. Esta arquitectura proporciona un nivel bueno de seguridad y ayuda a evitar que usuarios no autorizados pasen por alto la seguridad del firewall. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

