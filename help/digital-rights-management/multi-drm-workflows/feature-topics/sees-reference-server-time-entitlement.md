---
description: Trabaje con SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.
title: Derecho basado en el tiempo del servicio de referencia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Servicio de referencia: Derecho basado en el tiempo {#reference-service-time-based-entitlement}

Trabaje con SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.

El SEES recibe una solicitud de derecho (consulte la sección API pública ) del cliente. El servidor SEES busca el CEK y IV en función del `contentID`, agrega el `expirationTime` y reenvía la solicitud al servidor ExpressPlay. El token final de ExpressPlay está sujeto a tiempo. Consulte el diagrama de secuencia de derechos basados en tiempo a continuación. ![](assets/fees-time-based.png)

**Tabla 1: Parámetros de licencia enviados por el cliente**

| Parámetro de consulta | Descripción | Requerido |
|---|---|---|
| `contentKey` | Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido | Sí |
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
   <td>Hora de caducidad de este token. Este valor debe ser una cadena con formato de fecha y hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> en el indicador de zona "Z" ("Hora de Zulu") o un número entero precedido por un signo "+". Un ejemplo de fecha y hora RFC 3339 es <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Si el valor es una cadena en formato de fecha y hora RFC 3339, representa una fecha y hora de caducidad absoluta para el token. Si el valor es un número entero precedido por un signo "+", se interpreta como un número relativo de segundos desde la publicación que el token es válido. Por ejemplo, <span class="codeph"> +60</span> especifica un minuto. La duración máxima del token (y la predeterminada, si no se especifica) es de 30 días. Utilice el formulario codificado "%2B" al especificar el signo "+". </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

