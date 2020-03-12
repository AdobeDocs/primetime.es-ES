---
description: La interfaz de token de licencia de Widevine proporciona servicios de producción y prueba.
seo-description: La interfaz de token de licencia de Widevine proporciona servicios de producción y prueba.
seo-title: Solicitud o respuesta de token de licencia de Widevine
title: Solicitud o respuesta de token de licencia de Widevine
uuid: a3522422-7075-49a7-bc55-137ef84ee430
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Solicitud o respuesta de token de licencia de Widevine {#widevine-license-token-request-response}

La interfaz de token de licencia de Widevine proporciona servicios de producción y prueba.

Esta solicitud HTTP devuelve un token que se puede canjear por una licencia Widevine.

**Método: GET, POST** (con un cuerpo con codificación www-url que contiene parámetros para ambos métodos)

**Direcciones URL:**

* **Producción:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Prueba:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Solicitud de muestra:**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **Respuesta de muestra:**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Cuadro 13: Parámetros de consulta de token**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parámetro de consulta</b> </th> 
   <th class="entry"> <b>Descripción</b> </th> 
   <th class="entry"> <b>¿Requerido?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>Ésta es la clave de API del cliente, una para los entornos de producción y prueba. Puede encontrarlo en la ficha Panel de administración de ExpressPlay. </p> </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> Tanto <span class="codeph"> html </span> como <span class="codeph"> json </span>. <p>Si <span class="codeph"> html </span> (valor predeterminado), se proporciona una representación HTML de cualquier error en el cuerpo de entidad de la respuesta. Si <span class="codeph"> se especifica json </span> , se devuelve una respuesta estructurada en formato JSON. Consulte Errores <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON </a> para obtener más información. </p> <p>El tipo de MIME de la respuesta es <span class="codeph"> text/uri-list </span> en caso de éxito, <span class="codeph"> text/html </span> en formato de error <span class="codeph"> html </span> o <span class="codeph"> application/json </span> en formato de error <span class="codeph"> json </span> . </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 14: Parámetros de consulta de licencia**

| Parámetro de consulta | Descripción | ¿Requerido? |
|--- |--- |--- |
| `generalFlags` | Una cadena hexadecimal de 4 bytes que representa los indicadores de licencia. ‘0000&#39; es el único valor permitido | No |
| `kek` | Clave de cifrado de clave (KEK). Las claves se almacenan cifradas con un KEK mediante un algoritmo de ajuste de claves (AES Key Wrap, RFC3394). | No |
| `kid` | Una representación de cadena hexadecimal de 16 bytes de la clave de codificación de contenido o una cadena `^somestring'`. La longitud de la cadena seguida por el `^` no puede ser buena en 64 caracteres. Consulte la siguiente nota para ver un ejemplo. | Sí |
| `ek` | Una representación de cadena hexadecimal de la clave de contenido cifrado. | No |
| `contentKey` | Una representación de cadena hexadecimal de 16 bytes de la clave de codificación de contenido | Sí, a menos que `kek` se proporcione y `ek` o `kid` |
| `contentId` | ID de contenido | No |
| `securityLevel` | Los valores permitidos son 1-5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Sí |
| `hdcpOutputControl` | Los valores permitidos son 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Sí |
| `licenseDuration` * | Duración de la licencia en segundos. Si no se proporciona, indica que no hay límite en la duración. Consulte la nota siguiente para obtener información detallada. | No |
| `wvExtension` | Extensión abreviada de ajuste de formularioType y extensionPayload, como cadena separada por comas. Consulte el formato siguiente. Ejemplo: `…&wvExtension=wudo,AAAAAA==&…` | No, se puede utilizar cualquier número |

Acerca de `licenseDuration`: <ol><li> La reproducción se detendrá `licenseDuration` segundos después del inicio de la reproducción. </li><li> Para permitir que la reproducción se detenga/reanude durante un tiempo ilimitado, omita `licenseDuration` (el valor predeterminado será infinito). De lo contrario, especifique la cantidad de tiempo durante el cual los usuarios finales deben poder disfrutar del flujo. </li></ol>

**Cuadro 15: Parámetros de consulta de restricción de tokens**

| Parámetro de consulta | Descripción | ¿Requerido? |
|--- |--- |--- |
| `expirationTime` | Hora de caducidad de este token. Este valor DEBE ser una cadena en formato de fecha y hora [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) en el indicador de zona ‘Z’ (&quot;Hora de zulu&quot;) o un entero precedido por un signo +. Un ejemplo de fecha y hora RFC 3339 es 2006-04-14T12:01:10Z. <br> Si el valor es una cadena en formato de fecha y hora [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) , representa una fecha y hora de caducidad absoluta para el token. Si el valor es un entero precedido de un signo +, se interpreta como un número relativo de segundos, desde la emisión, que el token es válido. Por ejemplo, `+60` especifica un minuto. <br> La duración máxima y predeterminada del token (si no se especifica) es de 30 días. | No |

**Cuadro 16: Parámetros de consulta de correlación**

| **Parámetro de consulta** | **Descripción** | **¿Requerido?** |
|---|---|---|
| `cookie` | Cadena arbitraria de hasta 32 caracteres que se incluye en el token y se registra en el servidor de canje de tokens. Se puede utilizar para correlacionar entradas de registro en el servidor de canje y en los servidores del proveedor de servicios. | No |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Cuadro 17: Respuesta HTTP**

| **Código de estado HTTP** | **Descripción** | **Content-Type** | **El cuerpo de la entidad contiene** |
|---|---|---|---|
| `200 OK` | Sin errores. | `text/uri-list` | URL de adquisición de licencia + token |
| `400 Bad Request` | Argumentos no válidos | `text/html` o `application/json` | Descripción del error |
| `401 Unauthorized` | Error de autenticación | `text/html` o `application/json` | Descripción del error |
| `404 Not found` | Dirección URL incorrecta | `text/html` o `application/json` | Descripción del error |
| `50x Server Error` | Error del servidor | `text/html` o `application/json` | Descripción del error |

**Cuadro 18: Códigos de error de evento**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> Código </th> 
   <th class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Hora de caducidad del token no válida: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> Dirección IP no válida </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> Clave de cifrado de contenido no válida: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> Se especificaron indicadores de control de salida no válidos: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Se debe proporcionar el token de autenticación </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Distintivo de autenticación no válido: &lt;details&gt; <p>Nota:  Esto puede suceder si el autenticador es incorrecto o al acceder a la API de prueba en *.test.express.com usando el autenticador de producción y viceversa. </p> <p importance="high">Nota:  El SDK de Test y la herramienta de prueba avanzada (ATT) solo funcionan con <span class="filepath"> *.test.express.com </span>, mientras que los dispositivos de producción deben utilizar <span class="filepath"> *.service.express.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> No hay suficientes tokens disponibles </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Falta el tiempo de finalización del período de alquiler </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Falta la duración de la reproducción de alquiler </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Duración de reproducción de alquiler no válida </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> La clave de cifrado de contenido debe tener una longitud de 32 dígitos hexadecimales </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Error de administración de ExpressPlay: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Cuenta de servicio deshabilitada </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Cookie no válida </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Control de salida no válido, valores fuera del rango especificado </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> No se especificó ningún valor correspondiente </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> El tipo de extensión debe tener 4 caracteres </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> La carga útil de extensión debe estar codificada en Base64 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag </span> debe codificarse en 4 bytes </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Se especificó un formato de error no válido: &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> No se pudo autenticar el dispositivo </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> Token no válido </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> Niño <span class="filepath"> perdido </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> No se pudo obtener la clave de contenido del servicio de almacenamiento clave </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> kid </span> debe tener 32 caracteres hexadecimales </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> el niño </span> debe tener 64 caracteres después de la etiqueta '^' </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Niño <span class="codeph"> no válido </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Clave o <span class="codeph"> clave cifrada no válida </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Indicadores generales no válidos </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Datos de clave no válidos especificados </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Se especificó una duración de alquiler no válida </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> El enlace de ID de dispositivo no es compatible con Widevine </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> Falta el valor del nivel de seguridad </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> Valor de nivel de seguridad no válido </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> Falta el valor de control de salida HDCP </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Se especificó una duración de licencia no válida </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> No se pudo generar la licencia de Widevine </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Parámetros <span class="codeph"> de WVExtension no válidos </span> especificados </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Opción Widevine desactivada </td> 
  </tr> 
 </tbody> 
</table>