---
description: Las vulnerabilidades de seguridad de red son una de las primeras amenazas a cualquier servidor de aplicaciones orientado a Internet o a intranet, y debe endurecer los hosts de la red frente a estas vulnerabilidades.
title: Seguridad de capa de red
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Seguridad de capa de red{#network-layer-security}

Las vulnerabilidades de seguridad de red son una de las primeras amenazas a cualquier servidor de aplicaciones orientado a Internet o a intranet, y debe endurecer los hosts de la red frente a estas vulnerabilidades.

Estas son algunas técnicas comunes que reducen las vulnerabilidades de seguridad de la red:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Técnica </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Zonas desmilitarizadas (DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentación debe existir en al menos dos niveles con el servidor de aplicaciones que se utiliza para ejecutar Adobe Primetime DRM cuando Primetime DRM está detrás del cortafuegos interno. Debe separar la red externa de la DMZ que incluye los servidores web, y los servidores web deben separarse de la red interna. Puede utilizar cortafuegos para implementar estas capas de separación. </p> <p>Puede categorizar y controlar el tráfico que pasa por cada capa de red para garantizar que solo se permita el mínimo absoluto de datos necesarios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Direcciones IP privadas </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice Traducción de direcciones de red (NAT) con direcciones IP privadas RFC 1918 en servidores de aplicaciones DRM de Primetime. Puede asignar direcciones IP privadas (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) para que sea más difícil para un atacante enrutar el tráfico hacia y desde un host interno NAT a través de Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A continuación se indican algunos criterios que se deben tener en cuenta al seleccionar una solución de cortafuegos: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implemente firewalls que admitan servidores proxy o inspección de estado, en lugar de soluciones sencillas de filtrado de paquetes. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Utilice un cortafuegos que admita un paradigma de seguridad en el que puede denegar todos los servicios, excepto los servicios explícitamente permitidos. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implemente una solución de firewall que tenga dos hogares o varios hogares. Esta arquitectura proporciona el nivel bueno de seguridad y evita que los usuarios no autorizados pasen por alto la seguridad del firewall. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

