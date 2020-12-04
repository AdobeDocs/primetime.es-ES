---
description: Trabaje con SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.
seo-description: Trabaje con SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.
seo-title: Asignación de derechos basada en el tiempo del servicio de referencia
title: Asignación de derechos basada en el tiempo del servicio de referencia
uuid: dd937299-a271-49a9-9b26-eec16f1484df
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Servicio de referencia: Asignación de derechos basada en el tiempo {#reference-service-time-based-entitlement}

Trabaje con SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.

El SEES recibe una solicitud de asignación de derechos (consulte la sección API pública) del cliente. El servidor SEES busca el CEK y IV en base al `contentID`, agrega el `expirationTime` y reenvía la solicitud al servidor ExpressPlay. El token de ExpressPlay final está sujeto a tiempo. Consulte el diagrama de secuencia de asignación de derechos basada en tiempo que aparece a continuación. ![](assets/fees-time-based.png)

**Tabla 1: Parámetros de licencia enviados por el cliente**

| Parámetro de consulta | Descripción | Requerido |
|---|---|---|
| `contentKey` | Una representación de cadena hexadecimal de 16 bytes de la clave de codificación de contenido | Sí |
| `iv` | Una representación de cadena hexadecimal de 16 bytes del cifrado de contenido IV | Sí |
| `rentalDuration` | Duración del alquiler en segundos (predeterminado = 0) | No |

**Tabla 2: Parámetros de restricción de tokens agregados por el servidor SEES**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> Parámetro de consulta </th> 
   <th class="entry"> Descripción </th> 
   <th class="entry"> ¿Requerido? </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>Hora de caducidad de este token. Este valor debe ser una cadena con formato de fecha y hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> en el indicador de zona 'Z' ("Zulu time") o un entero precedido por un signo '+'. Un ejemplo de fecha y hora RFC 3339 es <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Si el valor es una cadena en formato de fecha y hora RFC 3339, representa una fecha y hora de caducidad absoluta para el token. Si el valor es un entero precedido por un signo '+', se interpreta como un número relativo de segundos desde la emisión que el token es válido. Por ejemplo, <span class="codeph"> +60</span> especifica un minuto. La duración máxima (y predeterminada, si no se especifica) del token es de 30 días. Utilice el formulario codificado "%2B" al especificar el signo "+". </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

