---
title: Información de seguridad específica del proveedor
description: Información de seguridad específica del proveedor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Información de seguridad específica del proveedor{#vendor-specific-security-information}

Esta sección contiene información relacionada con la seguridad sobre los sistemas operativos y los servidores de aplicaciones que se incorporan a su solución de acceso a Adobe.

Utilice los vínculos proporcionados en esta sección para encontrar información de seguridad específica del proveedor para su sistema operativo y servidor de aplicaciones.

## Información de seguridad del sistema operativo {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Al proteger el sistema operativo, implemente cuidadosamente las medidas que describe el proveedor del sistema operativo, incluidas las siguientes:

* Definición y control de usuarios, funciones y privilegios
* Monitorización de registros y pistas de auditoría
* Eliminación de servicios y aplicaciones innecesarios
* Copia de seguridad de archivos

Para obtener información de seguridad sobre los sistemas operativos compatibles con Adobe Access, consulte los recursos de esta tabla.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
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

En la tabla siguiente se describen algunos enfoques posibles para minimizar las vulnerabilidades de seguridad que se encuentran en el sistema operativo.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Elemento </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Revisiones de seguridad </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Existe un mayor riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones si los parches y las actualizaciones de seguridad del proveedor no se aplican de manera oportuna. Pruebe parches de seguridad antes de aplicarlos a los servidores de producción. </p> <p class="- topic/p ">Además, cree políticas y procedimientos para buscar e instalar parches de forma regular. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de protección antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Los analizadores de virus pueden identificar los archivos infectados mediante la búsqueda de una firma o la observación de comportamientos inusuales. Los escáneres guardan sus firmas de virus en un archivo, que generalmente se almacena en el disco duro local. Debido a que se descubren nuevos virus con frecuencia, debe actualizar este archivo para que el analizador de virus identifique todos los virus actuales. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Protocolo de tiempo de red (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para realizar el correcto funcionamiento y realizar análisis forenses, mantenga un tiempo preciso en los servidores de acceso al Adobe y en los paquetes de acceso al Adobe. Utilice una versión segura de NTP para sincronizar la hora en todos los sistemas conectados a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Información de seguridad del servidor de aplicaciones {#section-EBB4EF371CFF4A848694CC240B23D404}

Al proteger el servidor de aplicaciones, debe implementar las medidas que describe el proveedor del servidor, entre ellas:

* Uso de nombres de usuario de administrador no obvios
* Desactivación de servicios innecesarios
* Protección del administrador de la consola
* Habilitar cookies seguras
* Cierre de puertos innecesarios
* Limitación de interfaces administrativas por direcciones IP o dominios
* Uso del Administrador de seguridad de Java™

