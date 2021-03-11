---
title: Protocolos de red utilizados por el acceso a Adobe
description: Protocolos de red utilizados por el acceso a Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Protocolos de red utilizados por Acceso a Adobe {#network-protocols-used-by-adobe-access}

Al configurar una arquitectura de red segura, los protocolos de red de la siguiente tabla son necesarios para interactuar entre Adobe Access y otros sistemas de la red empresarial.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocolo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Uso </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player , Adobe AIR® y Adobe Primetime se comunican con Acceso a Adobe a través de HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR y Adobe Primetime pueden utilizar HTTPS para la comunicación con acceso a Adobe. Sin embargo, HTTPS (SSL) no es necesario a menos que necesite compatibilidad con clientes de FMRMS 1.x. Consulte las notas de la tabla <a href="network-topology-firewall-rules.md" format="dita" scope="local"> Direcciones URL entrantes</a> y <a href="network-topology-nw-protocols.md"> Configuración de SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>