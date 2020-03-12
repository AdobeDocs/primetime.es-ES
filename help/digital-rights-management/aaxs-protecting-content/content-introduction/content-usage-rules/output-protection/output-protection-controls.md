---
seo-title: Controles de protección de salida
title: Controles de protección de salida
uuid: 1f4cc617-7f14-4952-8e61-6acbdf01d10e
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Controles de protección de salida {#output-protection-controls}

**Controle si la salida a dispositivos de procesamiento externos está protegida. Especifique salidas analógicas y digitales de forma independiente.**

Controla si se debe restringir la salida a dispositivos de procesamiento externos. Un dispositivo externo se define como cualquier dispositivo de audio o vídeo que no esté incrustado en el equipo. La lista de dispositivos externos excluye las pantallas integradas, como en equipos portátiles. Las restricciones de salida analógica y digital se pueden especificar de forma independiente.

Existen las siguientes opciones y niveles de cumplimiento:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Compatible con dispositivos analógicos </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Compatible con dispositivos digitales </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obligatorio</b> — La protección de salida Analog Copy Protection (ACP) o Copy Generation Management System - Analog (CGMS-A) debe estar activada para poder reproducir contenido en un dispositivo externo. Los clientes de Adobe Access deben habilitar la protección de salida mediante ACP o CGMS-A. En los dispositivos que admiten ambos, los clientes de Adobe Access 3.0 intentarán habilitar ambos. Sin embargo, solo se debe habilitar uno para reproducir el contenido. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP requerido</b> — Se requiere protección de salida ACP. No se permite la reproducción en CGMS-A. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se establece, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin reproducción". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A Requerido</b> — Se requiere protección de salida CGMS-A. No se permite la reproducción en ACP. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se establece, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin reproducción". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Utilícelo si está disponible</b> — Intente habilitar la protección de salida ACP y CGMS-A si está disponible y permitir la reproducción si no está disponible. Los clientes de Adobe Access 3.0 intentarán habilitar tanto ACP como CGMS-A, si es posible. Los clientes de Adobe Access 2.0 solo intentarán activar ACP o CGMS-A. Por ejemplo, el cliente de Adobe Access intentará habilitar tanto ACP como CGMS-A. Si el intento se realiza correctamente, la otra opción no se activará. Si el intento falla, se realizará un segundo intento para habilitar la otra opción. Incluso si ambos intentos fallan, el contenido se reproducirá de todos modos. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usar ACP si está disponible</b> — Intente habilitar la protección de salida ACP si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en CGMS-A. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se establece, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin protección". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Utilice CGMS-A si está disponible </b>— Intente activar la protección de salida CGMS-A si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en los países ACP. Los clientes de Adobe Access 2.0 no admiten esta opción. Si se establece, un cliente de Adobe Access 2.0 se comportará como si se hubiera especificado la opción "Sin protección". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sin protección</b> — No se aplica ninguna habilitación de protección de salida para salidas analógicas y digitales. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sin reproducción</b> : no permita la reproducción en un dispositivo externo para salidas analógicas y digitales. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÍ </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Aunque estas reglas se aplican de manera consistente en todas las plataformas, actualmente solo es posible activar de forma segura la protección de salida en las plataformas Windows. En otras plataformas (como Macintosh y Linux) no hay funciones de sistema operativo compatibles disponibles para aplicaciones de terceros.

Ejemplo de caso de uso: Parte del contenido puede exigir controles de protección de salida y el distribuidor de contenido puede establecer el nivel de protección. Si se especifica &quot;Requerido&quot; y se intenta reproducir en un Macintosh, el cliente no reproduce contenido en dispositivos externos. Sin embargo, el contenido se reproducirá en monitores internos.

Si se especifica &quot;Requerido&quot; y se intenta reproducir en Linux, el cliente no reproduce contenido en ningún dispositivo porque no es posible diferenciar entre dispositivos internos y externos.

Si especifica &quot;Usar si está disponible&quot;, la protección de salida se activa siempre que sea posible. Por ejemplo, en equipos Windows que admiten el protocolo de protección de salida certificado (COPP), el contenido se pasa con protección de salida a una pantalla externa. Este ejemplo se conoce a veces como &quot;control de salida seleccionable&quot;.
