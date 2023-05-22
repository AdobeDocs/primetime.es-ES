---
title: Controles de protección de salida
description: Controles de protección de salida
copied-description: true
exl-id: e27e49f9-9bc3-493f-a9ba-efe623694942
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Controles de protección de salida {#output-protection-controls}

**Controle si la salida a dispositivos de procesamiento externos está protegida. Especificar las salidas analógicas y digitales de forma independiente.**

Controla si la salida a dispositivos de procesamiento externos debe restringirse. Un dispositivo externo se define como cualquier dispositivo de vídeo o audio que no esté incrustado en el equipo. La lista de dispositivos externos excluye las pantallas integradas, como en los ordenadores portátiles. Las restricciones de salida analógica y digital pueden especificarse de forma independiente.

Están disponibles las siguientes opciones/niveles de aplicación:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Admitido en dispositivos analógicos </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Admitido en dispositivos digitales </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Requerido</b> — Protección de copia analógica (ACP) o Sistema de gestión de generación de copias: la protección de salida analógica (CGMS-A) debe habilitarse para reproducir contenido en un dispositivo externo. Los clientes de acceso de Adobe deben activar la protección de salida mediante ACP o CGMS-A. En dispositivos compatibles con ambos, los clientes de Adobe Access 3.0 intentarán habilitar ambos. Sin embargo, solo uno debe estar habilitado para reproducir el contenido. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP Necesario</b> — Se requiere protección de la salida ACP. No se permite la reproducción en CGMS-A. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se configura, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin reproducción". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Se requiere CGMS-A</b> — Se requiere protección de salida CGMS-A. No se permite la reproducción en ACP. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se configura, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin reproducción". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usar si está disponible</b> — Intente activar la protección de salida ACP y CGMS-A si está disponible y permitir la reproducción si no está disponible. Los clientes de Adobe Access 3.0 intentarán habilitar tanto ACP como CGMS-A, si es posible. Los clientes de Adobe Access 2.0 solo intentarán habilitar ACP o CGMS-A. Por ejemplo, el cliente de acceso de Adobe intentará habilitar ACP o CGMS-A. Si el intento se realiza correctamente, la otra opción no estará habilitada. Si el intento falla, se realizará un segundo intento para habilitar la otra opción. Incluso si ambos intentos fallan, el contenido se reproducirá de todos modos. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Utilizar ACP si está disponible</b> — Intentar activar la protección de salida ACP si está disponible, pero permitir la reproducción si no está disponible. La protección no está disponible en CGMS-A. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se configura, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin protección". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Utilice CGMS-A si está disponible </b>— Intente activar la protección de salida CGMS-A si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en ACP. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se configura, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin protección". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sin protección</b> — No se exige protección de salida para las salidas analógicas y digitales. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sin reproducción</b> : no permitir la reproducción en un dispositivo externo para salidas analógicas y digitales. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Aunque estas reglas se aplican de forma coherente en todas las plataformas, actualmente solo es posible activar de forma segura la protección de salida en las plataformas Windows. En otras plataformas (como Macintosh y Linux) no hay funciones de sistema operativo compatibles disponibles para aplicaciones de terceros.

Ejemplo de caso de uso: Algunos contenidos pueden exigir controles de protección de salida, y el distribuidor de contenido puede establecer el nivel de protección. Si se especifica &quot;Obligatorio&quot; y se intenta reproducir en un Macintosh, el cliente no reproduce contenido en dispositivos externos. Sin embargo, el contenido se reproduce en monitores internos.

Si se especifica &quot;Obligatorio&quot; y se intenta la reproducción en Linux, el cliente no reproduce contenido en ningún dispositivo porque no es posible diferenciar entre dispositivos internos y externos.

Si especifica &quot;Usar si está disponible&quot;, la protección de salida se activa siempre que sea posible. Por ejemplo, en equipos Windows que admiten el Protocolo de protección de salida certificada (COPP), el contenido se pasa con protección de salida a una pantalla externa. Este ejemplo se conoce a veces como &quot;control de salida seleccionable&quot;.
