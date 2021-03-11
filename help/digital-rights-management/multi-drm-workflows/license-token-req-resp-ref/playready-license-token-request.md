---
description: La interfaz de token de licencia PlayReady proporciona servicios de producción y prueba.
title: Solicitud/respuesta del token de licencia de PlayReady
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---


# Solicitud de token de licencia PlayReady/respuesta {#playready-license-token-request-response}

La interfaz de token de licencia PlayReady proporciona servicios de producción y prueba.

Esta solicitud HTTP devuelve un token que se puede canjear por una licencia PlayReady.

**Método: GET, POST**  (con un cuerpo con codificación www-url que contiene parámetros para ambos métodos)

**URL:**

* **Producción:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Prueba:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Solicitud de ejemplo:**

   ```
   <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
   https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
    <ExpressPlay customer authenticator identifier>
    &kid=<CEKSID>
    &contentKey=<CEK>
    &rightsType=BuyToOwn
    &analogVideoOPL=0
    &compressedDigitalAudioOPL=0
    &compressedDigitalVideoOPL=0
    &uncompressedDigitalAudioOPL=0
    &uncompressedDigitalVideoOPL=0
   </xref href="https:>
   ```

* **Respuesta de ejemplo:**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## Parámetros de consulta de solicitud {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Tabla 9: Parámetros de consulta de token**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parámetro de consulta</b> </th> 
   <th class="entry"><b>Descripción</b> </th> 
   <th class="entry"><b>¿Requerido?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>Esta es la clave de API del cliente, una para los entornos de producción y prueba. Puede encontrarlo en la pestaña del panel de administración de ExpressPlay. </p> </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td><span class="codeph"> html</span> o <span class="codeph"> json</span>. Si <span class="codeph"> html</span> (predeterminado) se proporciona una representación HTML de cualquier error en el cuerpo de la entidad de la respuesta. <p>Si se especifica <span class="codeph"> json</span> , se devuelve una respuesta estructurada en formato JSON. Consulte <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Errores JSON</a> para obtener más información. </p> <p>El tipo de MIME de la respuesta es <span class="codeph"> text/uri-list</span> on success, <span class="codeph"> text/html</span> para el formato de error HTML o <span class="codeph"> application/json</span> para el formato de error JSON. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 10: Parámetros de consulta de licencia**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parámetro de consulta</b> </th> 
   <th class="entry"><b>Descripción</b> </th> 
   <th class="entry"><b>¿Requerido?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>Cadena hexadecimal de 4 bytes que representa los indicadores de licencia. Debe establecerse en "00000001" para una licencia persistente. <p>Nota: Las licencias de alquiler (<span class="codeph"> rightsType=Rental</span>) DEBEN ser persistentes. </p> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> Clave de cifrado de claves (KEK). Las claves se almacenan cifradas con un KEK mediante un algoritmo de ajuste de claves (AES Key Wrap, RFC3394). </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> child</span> </td> 
   <td>Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido o una cadena <span class="codeph"> ^somestring'</span>. La longitud de la cadena seguida de '^' no puede tener buenos 64 caracteres. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> Una representación de cadena hexadecimal de la clave de contenido cifrada. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido </td> 
   <td>Sí, a menos que se proporcione <span class="codeph"> kek</span> y <span class="codeph"> ek</span> o <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Especifica el tipo de derechos. Debe ser <span class="codeph"> BuyToOwn</span> o <span class="codeph"> Alquiler</span>. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.periodEndTime</span> </td> 
   <td>Fecha de finalización del alquiler. Este valor DEBE tener el formato "RFC 3339" _ fecha/hora en el formato "Z" del indicador de zona ("Zulu time") o un número entero precedido de un signo "+". <p>Si el valor es un formato de fecha y hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a>, representa una fecha y hora de caducidad absoluta para la licencia. Un ejemplo de fecha y hora RFC 3339 es 2006-04-14T12:01:10Z. </p> <p> Si el valor es un número entero precedido por un signo "+", se toma como un número relativo de segundos desde el momento en que se emite el token. El contenido no se puede reproducir después de este tiempo. Solo es válido si <span class="codeph"> rightsType</span> es <span class="codeph"> Alquiler</span>. </p> </td> 
   <td>Sí, cuando <span class="codeph"> rightsType</span> es <span class="codeph"> Alquiler</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.playDuration</span> </td> 
   <td>Tiempo, en segundos, que el contenido se puede reproducir una vez iniciada la reproducción. Solo es válido si <span class="codeph"> rightsType</span> es Rental. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analógicoVideoOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para vídeo analógico. Intervalo válido 0-999. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> zipDigitalAudioOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para audio digital comprimido. Intervalo válido 0-999. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> zipDigitalVideoOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para vídeo digital comprimido. Intervalo válido 0-999. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unzipDigitalAudioOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para el audio digital sin comprimir. Intervalo válido 0-999. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unzipDigitalVideoOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para vídeo digital sin comprimir. Intervalo válido 0-999. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Comportamiento requerido cuando se desconoce el resultado. Valores permitidos: <span class="codeph"> Permitir</span>, <span class="codeph"> No permitir</span> o <span class="codeph"> SDOnly</span> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Un valor hexadecimal de 4 bytes para indicar los indicadores de otras opciones de control de salida </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Una palabra arbitraria de 4 letras que representa un identificador de 32 bits para una extensión. El código ASCII de 8 bits de cada letra es la parte correspondiente de 8 bits del identificador. Por ejemplo, el valor identificador 0x61626364 (hexadecimal) estaría escrito ‘<span class="codeph"> abcd</span>', porque el código ASCII para ‘a' es 0x61, etc. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Cadena codificada base64 de la extensión. </td> 
   <td>Sí, cuando se especifica <span class="codeph"> extensionType</span>. </td> 
  </tr> 
 </tbody> 
</table>

## Respuestas {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Tabla 11: Respuestas HTTP**

| **Código de estado HTTP** | **Descripción** | **Content-Type** | **El cuerpo de la entidad contiene** |
|---|---|---|---|
| `200 OK` | Sin error. | `text/uri-list` | URL y token de adquisición de licencia |
| `400 Bad Request` | Argumentos no válidos | `text/html` o  `application/json` | Descripción del error |
| `401 Unauthorized` | Error de autenticación | `text/html` o  `application/json` | Descripción del error |
| `404 Not found` | Dirección URL incorrecta | `text/html` o  `application/json` | Descripción del error |
| `50x Server Error` | Error del servidor | `text/html` o  `application/json` | Descripción del error |

**Tabla 12: Códigos de error de evento**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Código</b> </th> 
   <th class="entry"><b>Descripción</b> </th> 
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
   <td>Token de autenticación no válido: &lt;details&gt; <p>Nota:  Esto puede ocurrir si el autenticador es incorrecto o al acceder a la API de prueba en *.test.expression.com mediante el autenticador de producción y viceversa. </p> <p importance="high">Nota: El SDK de prueba y la herramienta de prueba avanzada (ATT) solo funcionan con <span class="filepath"> *.test.expression.com</span>, mientras que los dispositivos de producción deben utilizar <span class="filepath"> *.service.expression.com</span>. </p> </td> 
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
   <td><span class="codeph"> </span> OutputControlFlagmust be encode 4 bytes </td> 
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
   <td> -4018 </td> 
   <td>Falta <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Error al obtener la clave de contenido del servicio de almacenamiento clave </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> </span> kidmust be 32 hexadecimal length </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> </span> El archivo debe tener 64 caracteres después de ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td><span class="codeph"> kid</span> no válido </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Clave <span class="codeph"> cifrada</span> o kek no válida </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Error de tipo de salida desconocido no válido </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> La opción PlayReady está desactivada para este servicio </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Indicadores generales no válidos </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> El ID del dispositivo debe tener 32 caracteres hexadecimales </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> ID de dispositivo no válido </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> Falta el valor OPL </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>Solo se puede especificar uno de <span class="codeph"> kek</span> o <span class="codeph"> contentKey</span> </td> 
  </tr> 
 </tbody> 
</table>
