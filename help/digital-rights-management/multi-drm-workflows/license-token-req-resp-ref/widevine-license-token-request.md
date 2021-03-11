---
description: La interfaz de token de licencia Widevine proporciona servicios de producción y prueba.
title: Solicitud de token de licencia de Widevine/respuesta
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---


# Solicitud de token de licencia de Widevine/respuesta {#widevine-license-token-request-response}

La interfaz de token de licencia Widevine proporciona servicios de producción y prueba.

Esta solicitud HTTP devuelve un token que se puede canjear por una licencia Widevine.

**Método: GET, POST**  (con un cuerpo con codificación www-url que contiene parámetros para ambos métodos)

**URL:**

* **Producción:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Prueba:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Solicitud de ejemplo:**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **Respuesta de ejemplo:**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Tabla 13: Parámetros de consulta de token**

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
   <td> <span class="codeph"> customerAuthenticator  </span> </td> 
   <td> <p>Esta es la clave de API del cliente, una para los entornos de producción y prueba. Puede encontrarlo en la pestaña del panel de administración de ExpressPlay. </p> </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat  </span> </td> 
   <td> <span class="codeph"> html </span> o <span class="codeph"> json </span>. <p>Si <span class="codeph"> html </span> (predeterminado) se proporciona una representación HTML de cualquier error en el cuerpo de la entidad de la respuesta. Si se especifica <span class="codeph"> json </span> , se devuelve una respuesta estructurada en formato JSON. Consulte <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Errores JSON </a> para obtener más información. </p> <p>El tipo de mime de la respuesta es <span class="codeph"> text/uri-list </span> on success, <span class="codeph"> text/html </span> para <span class="codeph"> html </span> formato de error, o <span class="codeph"> application/json </span> para el formato de error <span class="codeph"> json </span>. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 14: Parámetros de consulta de licencia**

| Parámetro de consulta | Descripción | ¿Requerido? |
|--- |--- |--- |
| `generalFlags` | Cadena hexadecimal de 4 bytes que representa los indicadores de licencia. &quot;0000&quot; es el único valor permitido | No |
| `kek` | Clave de cifrado de claves (KEK). Las claves se almacenan cifradas con un KEK mediante un algoritmo de ajuste de claves (AES Key Wrap, RFC3394). | No |
| `kid` | Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido o una cadena `^somestring'`. La longitud de la cadena seguida de `^` no puede ser buena a 64 caracteres. Para ver un ejemplo, consulte la nota siguiente. | Sí |
| `ek` | Una representación de cadena hexadecimal de la clave de contenido cifrada. | No |
| `contentKey` | Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido | Sí, a menos que se proporcionen `kek` y `ek` o `kid` |
| `contentId` | ID de contenido | No |
| `securityLevel` | Los valores permitidos son del 1 al 5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Sí |
| `hdcpOutputControl` | Los valores permitidos son 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Sí |
| `licenseDuration` * | Duración de la licencia en segundos. Si no se proporciona, indica que no hay límite en la duración. Consulte la nota siguiente para obtener información detallada. | No |
| `wvExtension` | Un formulario corto que ajusta extensionType y extensionPayload como una cadena separada por comas. Consulte el formato a continuación. Ejemplo: `…&wvExtension=wudo,AAAAAA==&…` | No, se puede usar cualquier número |

Acerca de `licenseDuration`: <ol><li> La reproducción se detendrá `licenseDuration` segundos después del inicio de la reproducción. </li><li> Para permitir que la reproducción se detenga/reanude durante un tiempo ilimitado, omita `licenseDuration` (de forma predeterminada será infinita). De lo contrario, especifique la cantidad de tiempo durante el cual los usuarios finales deben poder disfrutar de la emisión. </li></ol>

**Tabla 15: Parámetros de consulta de restricción de tokens**

| Parámetro de consulta | Descripción | ¿Requerido? |
|--- |--- |--- |
| `expirationTime` | Hora de caducidad de este token. Este valor DEBE ser una cadena con el formato de fecha y hora [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) en el indicador de zona &quot;Z&quot; (&quot;Hora de Zulu&quot;) o un número entero precedido por un signo +. Un ejemplo de fecha y hora RFC 3339 es 2006-04-14T12:01:10Z. <br> Si el valor es una cadena en formato de fecha y hora  [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) , representa una fecha y hora de caducidad absoluta para el token. Si el valor es un entero precedido por un signo +, se interpreta como un número relativo de segundos, desde la publicación, que el token es válido. Por ejemplo, `+60` especifica un minuto. <br> La duración máxima y predeterminada del token (si no se especifica) es de 30 días. | No |

**Tabla 16: Parámetros de consulta de correlación**

| **Parámetro de consulta** | **Descripción** | **¿Requerido?** |
|---|---|---|
| `cookie` | Cadena arbitraria de hasta 32 caracteres llevada en el token y registrada por el servidor de canje de tokens. Se puede utilizar para correlacionar entradas de registro en el servidor de canje y en los servidores del proveedor de servicios. | No |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Tabla 17: Respuesta HTTP**

| **Código de estado HTTP** | **Descripción** | **Content-Type** | **El cuerpo de la entidad contiene** |
|---|---|---|---|
| `200 OK` | Sin error. | `text/uri-list` | URL de adquisición de licencia + token |
| `400 Bad Request` | Argumentos no válidos | `text/html` o  `application/json` | Descripción del error |
| `401 Unauthorized` | Error de autenticación | `text/html` o  `application/json` | Descripción del error |
| `404 Not found` | Dirección URL incorrecta | `text/html` o  `application/json` | Descripción del error |
| `50x Server Error` | Error del servidor | `text/html` o  `application/json` | Descripción del error |

**Tabla 18: Códigos de error de evento**

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
   <td> Indicadores de control de salida no válidos especificados: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Se debe proporcionar el token de autenticación </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Token de autenticación no válido: &lt;details&gt; <p>Nota:  Esto puede ocurrir si el autenticador es incorrecto o al acceder a la API de prueba en *.test.expression.com mediante el autenticador de producción y viceversa. </p> <p importance="high">Nota:  El SDK de prueba y la herramienta de prueba avanzada (ATT) solo funcionan con <span class="filepath"> *.test.expression.com </span>, mientras que los dispositivos de producción deben utilizar <span class="filepath"> *.service.expression.com </span> </p>. </td> 
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
   <td> La clave de cifrado de contenido debe tener 32 dígitos hexadecimales </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Error del administrador de ExpressPlay: &lt;details&gt; </td> 
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
   <td> No se ha especificado ningún valor correspondiente </td> 
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
   <td> <span class="codeph"> OutputControlFlag  </span> debe estar codificado 4 bytes </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Formato de error especificado no válido: &lt;formato&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> El dispositivo no se ha podido autenticar </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> Token no válido </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> Falta <span class="filepath"> secundario </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Error al obtener la clave de contenido del servicio de almacenamiento clave </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> El elemento secundario  </span> debe tener 32 caracteres hexadecimales </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> El chico  </span> debe tener 64 caracteres después de '^' </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> <span class="codeph"> de </span> no válido </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Clave cifrada no válida o clave <span class="codeph"> </span> no válida </td> 
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
   <td> No se pudo generar la licencia Widevine </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Parámetros de <span class="codeph"> WVEextension </span> no válidos especificados </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Opción Widevine desactivada </td> 
  </tr> 
 </tbody> 
</table>