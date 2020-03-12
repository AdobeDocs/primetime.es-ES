---
seo-title: Protocolos de red utilizados por Adobe Access
title: Protocolos de red utilizados por Adobe Access
uuid: 4f2ee3f5-6758-4fbe-b5cd-cead1e5ccde8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Protocolos de red utilizados por Adobe Access {#network-protocols-used-by-adobe-access}

Al configurar una arquitectura de red segura, los protocolos de red de la siguiente tabla son necesarios para la interacción entre Adobe Access y otros sistemas de la red empresarial.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocolo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Usar </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR® y Adobe Primetime se comunican con Adobe Access a través de HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los clientes de Flash Player, Adobe AIR y Adobe Primetime pueden utilizar HTTPS para la comunicación con Adobe Access; sin embargo, HTTPS (SSL) no es necesario a menos que necesite asistencia para los clientes de FMRMS 1.x. Consulte las notas en la tabla <a href="network-topology-firewall-rules.md" format="dita" scope="local"> Direcciones URL</a> entrantes y <a href="network-topology-nw-protocols.md"> Configuración de SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>