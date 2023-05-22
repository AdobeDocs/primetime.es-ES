---
description: Trabaje con el SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.
title: Derecho basado en tiempo del servicio de referencia
exl-id: a37b0e71-ba7b-4f03-9866-5e8b062e0b7d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Servicio de referencia: derecho basado en el tiempo {#reference-service-time-based-entitlement}

Trabaje con el SEES para ver cómo habilitar un servicio de asignación de derechos basado en el tiempo mediante ExpressPlay.

El SEES recibe una solicitud de derecho (consulte la sección API pública ) del cliente. El servidor SEES busca la CEK y la IV en función de la `contentID`, añade el `expirationTime`y reenvía la solicitud al servidor de ExpressPlay. El token final de ExpressPlay tiene un límite de tiempo. Consulte el diagrama de secuencia de derechos basados en tiempo a continuación. ![](assets/fees-time-based.png)

**Tabla 1: Parámetros de licencia enviados por el cliente**

| Parámetro de consulta | Descripción | Requerido |
|---|---|---|
| `contentKey` | Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido | Sí |
| `iv` | Una representación de cadena hexadecimal de 16 bytes del cifrado de contenido IV | Sí |
| `rentalDuration` | Duración del alquiler en segundos (predeterminado = 0) | No |

**Tabla 2: Parámetros de restricción de tokens añadidos por el servidor SEES**

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
   <td>Hora de caducidad de este token. Este valor debe ser una cadena en <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> formato de fecha y hora en el designador de zona "Z" ("hora zulú") o un entero precedido por el signo "+". Un ejemplo de fecha/hora RFC 3339 es <span class="codeph"> 14-04-2006:01:10Z</span>. <p>Si el valor es una cadena en formato de fecha/hora RFC 3339, representa una fecha/hora de caducidad absoluta para el token. Si el valor es un entero precedido por el signo "+", se interpreta como un número relativo de segundos desde la emisión que el token es válido. Por ejemplo, <span class="codeph"> +60</span> especifica un minuto. La duración máxima del token (y la predeterminada, si no se especifica) es de 30 días. Utilice el formulario codificado "%2B" al especificar el signo +. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>
