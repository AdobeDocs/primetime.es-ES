---
description: Los sistemas operativos y los servidores de aplicaciones están incluidos en la solución DRM de Adobe Primetime.
title: Información de seguridad específica del proveedor
exl-id: 4cc39414-cab5-4282-825d-64651d9b03e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Información de seguridad específica del proveedor{#vendor-specific-security-information}

Los sistemas operativos y los servidores de aplicaciones están incluidos en la solución DRM de Adobe Primetime.

Para obtener información de seguridad específica del proveedor para el sistema operativo y el servidor de aplicaciones, consulte Uso del servidor de claves DRM de Adobe Primetime.

## Información de seguridad del sistema operativo {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

A la hora de proteger el sistema operativo, debe implementar las medidas descritas por el proveedor del sistema operativo.

Estas son algunas de las medidas:

* Definición y control de usuarios, funciones y privilegios
* Monitorización de registros y pistas de auditoría
* Eliminación de servicios y aplicaciones innecesarios
* Copia de seguridad de archivos

A continuación se proporciona información sobre los sistemas operativos compatibles con DRM de Adobe Primetime:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Sistema operativo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Recurso de seguridad </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise o Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guía de seguridad de Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 y 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guía de seguridad de Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

A continuación se proporciona información sobre los enfoques para minimizar las vulnerabilidades de seguridad en el sistema operativo:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Elemento </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Parches de seguridad </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones aumenta si los parches y las actualizaciones de seguridad del proveedor no se aplican de forma oportuna. </p> <p>Nota: Asegúrese de probar los parches de seguridad antes de aplicarlos a los servidores de producción. </p> <p class="- topic/p ">Debe crear políticas y procedimientos para comprobar e instalar los parches de forma regular. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de protección antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los analizadores de virus pueden identificar los archivos infectados mediante la búsqueda de una firma o un comportamiento inusual. </p> <p>Los analizadores guardan sus firmas de virus en un archivo que suele almacenarse en el disco duro local. Los nuevos virus se descubren con frecuencia, por lo que debe asegurarse de que este archivo se actualiza con regularidad. De este modo, los analizadores de virus siempre pueden identificar todos los virus actuales. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Protocolo de tiempo de red (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para un funcionamiento adecuado y análisis forense, mantenga la hora exacta en los servidores y empaquetadores DRM de Primetime. Utilice una versión segura de NTP para sincronizar la hora DRM de Primetime en todos los sistemas conectados a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Información de seguridad del servidor de aplicaciones {#section_22986936F1A547CEAB2D97E9E9D4825C}

A la hora de proteger el servidor de aplicaciones, debe implementar las medidas descritas por el proveedor del servidor.

Estas son algunas de estas medidas:

* Uso de nombres de usuario de administrador no obvios
* Desactivación de servicios innecesarios
* Protección del administrador de la consola
* Habilitar cookies seguras
* Cierre de puertos innecesarios
* Limitación de interfaces administrativas por direcciones IP o dominios
* Uso del Administrador de seguridad de Java™
