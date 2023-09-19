---
title: Protocolos de red utilizados por Acceso desde Adobe
description: Protocolos de red utilizados por Acceso desde Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Protocolos de red utilizados por Acceso desde Adobe {#network-protocols-used-by-adobe-access}

Cuando se configura una arquitectura de red segura, los protocolos de red de la tabla siguiente son necesarios para la interacción entre Acceso de Adobe y otros sistemas de la red empresarial.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocol </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Uso </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR® y Adobe Primetime se comunican con el acceso de Adobe a través de HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR y Adobe Primetime pueden utilizar HTTPS para la comunicación con el acceso de Adobe. Sin embargo, HTTPS (SSL) no es necesario a menos que necesite compatibilidad con clientes de FMRMS 1.x. Consulte las notas de la tabla <a href="network-topology-firewall-rules.md" format="dita" scope="local"> URL entrantes</a> y <a href="network-topology-nw-protocols.md"> Configuración de SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
