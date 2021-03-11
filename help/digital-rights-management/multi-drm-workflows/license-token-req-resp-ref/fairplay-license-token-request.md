---
description: La interfaz de token de licencia de FairPlay proporciona servicios de producción y prueba.
title: Solicitud/respuesta del token de licencia de FairPlay
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 5%

---


# Solicitud y respuesta del token de licencia de FairPlay {#fairplay-license-token-request-response}

La interfaz de token de licencia de FairPlay proporciona servicios de producción y prueba. Esta solicitud devuelve un token que se puede canjear por una licencia de FairPlay.

**Método: GET, POST**  (con un cuerpo con codificación www-url que contiene parámetros para ambos métodos)

**URL:**

* **Producción:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Prueba:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **Solicitud de ejemplo:**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **Respuesta de ejemplo:**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**Parámetros de consulta de solicitud**

**Tabla 3: Parámetros de consulta de token**

| Parámetro de consulta | Descripción | ¿Requerido? |
|--- |--- |--- |
| CustomerAuthenticator Customer Authentication como parámetro de consulta customerAuthenticator FairPlay | Esta es la clave de API del cliente, una para los entornos de producción y prueba. Puede encontrarlo en la pestaña del panel de administración de ExpressPlay. | Sí |
| errorFormat | Tanto html como json. Si html (el valor predeterminado), se proporciona una representación HTML de cualquier error en el cuerpo de la entidad de la respuesta. Si se especifica json, se devuelve una respuesta estructurada en formato JSON. Consulte [Errores JSON](https://www.expressplay.com/developer/restapi/#json-errors) para obtener más información. El tipo de mime de la respuesta es text/uri-list on success, text/html para el formato de error HTML o application/json para el formato de error JSON. | No |

**Tabla 4: Parámetros de consulta de licencia**

| **Parámetro de consulta** | **Descripción** | **¿Requerido?** |
|---|---|---|
| `generalFlags` | Cadena hexadecimal de 4 bytes que representa los indicadores de licencia. &quot;0000&quot; es el único valor permitido. | No |
| `kek` | Clave de cifrado de claves (KEK). Las claves se almacenan cifradas con un KEK mediante un algoritmo de ajuste de claves (AES Key Wrap, RFC3394). Si se proporciona `kek`, es necesario proporcionar uno de los parámetros `kid` o `ek`, *pero no ambos*. | No |
| `kid` | Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido o una cadena `'^somestring'`. La longitud de la cadena seguida de `'^'` no puede ser buena a 64 caracteres. | No |
| `ek` | Una representación de cadena hexadecimal de la clave de contenido cifrada. | No |
| `contentKey` | Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido | Sí, a menos que se proporcionen los `kek` y `ek` o `kid`. |
| `iv` | Una representación de cadena hexadecimal de 16 bytes del cifrado de contenido IV | Sí |
| `rentalDuration` | Duración del alquiler en segundos (predeterminado - 0) | No |
| `fpExtension` | Un formulario corto que ajusta `extensionType` y `extensionPayload` como una cadena separada por comas. Por ejemplo: […] `&fpExtension=wudo,AAAAAA==&`[…] | No, se puede usar cualquier número |

**Tabla 5: Parámetros de consulta de restricción de tokens**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parámetro de consulta</b> </th> 
   <th class="entry"> <b>Descripción</b> </th> 
   <th class="entry"> <b>¿Requerido?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime  </span> </td> 
   <td> Hora de caducidad de este token. Este valor DEBE ser una cadena en formato <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> de fecha y hora en el indicador de zona "Z" ("Hora de Zulu") o un número entero precedido por un signo "+". Un ejemplo de fecha y hora RFC 3339 es <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>Si el valor es una cadena en formato <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> de fecha y hora, representa una fecha y hora de caducidad absoluta para el token. Si el valor es un número entero precedido por un signo "+", se interpreta como un número relativo de segundos, desde la publicación, que el token es válido. </p> Por ejemplo, <span class="codeph"> +60 </span> especifica un minuto. La duración máxima y predeterminada del token (si no se especifica) es de 30 días. </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 6: Parámetros de consulta de correlación**

| **Parámetro de consulta** | **Descripción** | **¿Requerido?** |
|---|---|---|
| `cookie` | Cadena arbitraria de hasta 32 caracteres, que se lleva en el token y se registra en el servidor de canje de tokens. Esto se puede utilizar para correlacionar entradas de registro en el servidor de canje y en los servidores del proveedor de servicios. | No |

**Respuesta**

**Tabla 7: Respuestas HTTP**

| **Código de estado HTTP** | **Descripción** | **Content-Type** | **El cuerpo de la entidad contiene** |
|---|---|---|---|
| `200 OK` | Sin error. | `text/uri-list` | URL de adquisición de licencia + token |
| `400 Bad Request` | Argumentos no válidos | `text/html` o  `application/json` | Descripción del error |
| `401 Unauthorized` | Error de autenticación | `text/html` o  `application/json` | Descripción del error |
| `404 Not found` | Dirección URL incorrecta | `text/html` o  `application/json` | Descripción del error |
| `50x Server Error` | Error del servidor | `text/html` o  `application/json` | Descripción del error |

**Tabla 8: Códigos de error de evento**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Código</b> </th> 
   <th class="entry"> <b>Descripción</b> </th> 
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
   <td> Token de autenticación no válido: &lt;details&gt; <p>Nota:  Esto puede suceder si el autenticador es incorrecto o al acceder a la API de prueba en <span class="filepath"> *.test.expression.com </span> utilizando el autenticador de producción y viceversa. </p> <p importance="high">Nota:  El SDK de prueba y la herramienta de prueba avanzada (ATT) solo funcionan con <span class="filepath"> *.test.expression.com </span>, mientras que los dispositivos de producción deben utilizar <span class="filepath"> *.service.expression.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> No hay suficientes tokens disponibles </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> Falta el tipo de derechos </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> Tipo de derechos no válido </td> 
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
   <td> Falta un hijo </td> 
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
   <td> <span class="codeph"> El chico  </span> debe tener 64 caracteres después de ^ </td> 
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
   <td> -6001 </td> 
   <td> Parámetros de <span class="codeph"> FPEextension </span> no válidos especificados </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> Tipo de token de FP no válido </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Parámetro <span class="codeph"> iv </span> no válido especificado </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> No se pudo generar CKC para FP </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Datos de clave no válidos especificados </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> Servicio no autorizado para soporte de FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Se especificó una duración de alquiler no válida </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> El enlace de ID de dispositivo no es compatible con FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> Opción FairPlay desactivada </td> 
  </tr> 
 </tbody> 
</table>