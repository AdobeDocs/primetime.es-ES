---
description: Los sistemas operativos y los servidores de aplicaciones están incluidos en su solución Adobe Primetime DRM.
title: Información de seguridad específica del proveedor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Información de seguridad específica del proveedor{#vendor-specific-security-information}

Los sistemas operativos y los servidores de aplicaciones están incluidos en su solución Adobe Primetime DRM.

Para encontrar información de seguridad específica del proveedor para su sistema operativo y servidor de aplicaciones, consulte Uso del servidor de claves DRM de Adobe Primetime.

## Información de seguridad del sistema operativo {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

Al proteger el sistema operativo, debe implementar las medidas que describe el proveedor del sistema operativo.

Estas son algunas de las medidas:

* Definición y control de usuarios, funciones y privilegios
* Monitorización de registros y pistas de auditoría
* Eliminación de servicios y aplicaciones innecesarios
* Copia de seguridad de archivos

A continuación se proporciona información sobre los sistemas operativos compatibles con Adobe Primetime DRM:

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Revisiones de seguridad </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Existe un mayor riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones si los parches y las actualizaciones de seguridad del proveedor no se aplican de manera oportuna. </p> <p>Nota:  Asegúrese de probar los parches de seguridad antes de aplicarlos a los servidores de producción. </p> <p class="- topic/p ">Debe crear políticas y procedimientos para buscar e instalar parches con regularidad. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de protección antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los analizadores de virus pueden identificar los archivos infectados mediante la búsqueda de una firma o un comportamiento inusual. </p> <p>Los escáneres guardan sus firmas de virus en un archivo, que generalmente se almacena en el disco duro local. Con frecuencia se descubren nuevos virus, por lo que debe asegurarse de que este archivo se actualice con regularidad. De esta manera, los escáneres de virus siempre pueden identificar todos los virus actuales. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Protocolo de tiempo de red (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para un correcto funcionamiento y análisis forense, mantenga un tiempo preciso en los servidores y paquetes de Primetime DRM. Utilice una versión segura de NTP para sincronizar el tiempo de Primetime DRM en todos los sistemas conectados a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Información de seguridad del servidor de aplicaciones {#section_22986936F1A547CEAB2D97E9E9D4825C}

Al proteger el servidor de aplicaciones, debe implementar las medidas que describe el proveedor del servidor.

Estas son algunas de estas medidas:

* Uso de nombres de usuario de administrador no obvios
* Desactivación de servicios innecesarios
* Protección del administrador de la consola
* Habilitar cookies seguras
* Cierre de puertos innecesarios
* Limitación de interfaces administrativas por direcciones IP o dominios
* Uso del Administrador de seguridad de Java™

