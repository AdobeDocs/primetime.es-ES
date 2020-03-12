---
description: La interfaz del token de licencia de PlayReady proporciona servicios de producción y prueba.
seo-description: La interfaz del token de licencia de PlayReady proporciona servicios de producción y prueba.
seo-title: Solicitud o respuesta del token de licencia de PlayReady
title: Solicitud o respuesta del token de licencia de PlayReady
uuid: 20ebd582-ebb9-4716-8c1e-df3e58d6ec14
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Solicitud o respuesta del token de licencia de PlayReady {#playready-license-token-request-response}

La interfaz del token de licencia de PlayReady proporciona servicios de producción y prueba.

Esta solicitud HTTP devuelve un token que se puede canjear por una licencia de PlayReady.

**Método: GET, POST** (con un cuerpo con codificación www-url que contiene parámetros para ambos métodos)

**Direcciones URL:**

* **Producción:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Prueba:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Solicitud de muestra:**

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

* **Respuesta de muestra:**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## Parámetros de consulta de solicitud {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Cuadro 9: Parámetros de consulta de token**

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
   <td> <p>Ésta es la clave de API del cliente, una para los entornos de producción y prueba. Puede encontrarlo en la ficha Panel de administración de ExpressPlay. </p> </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>Tanto <span class="codeph"> html</span> como <span class="codeph"> json</span>. Si <span class="codeph"> html</span> (valor predeterminado), se proporciona una representación HTML de cualquier error en el cuerpo de entidad de la respuesta. <p>Si se especifica <span class="codeph"> json</span> , se devuelve una respuesta estructurada en formato JSON. Consulte Errores <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON</a> para obtener más información. </p> <p>El tipo de MIME de la respuesta es <span class="codeph"> text/uri-list</span> en caso de éxito, <span class="codeph"> text/html</span> en formato de error HTML o <span class="codeph"> application/json</span> en formato de error JSON. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 10: Parámetros de consulta de licencia**

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
   <td>Una cadena hexadecimal de 4 bytes que representa los indicadores de licencia. Debe establecerse en "00000001" para una licencia persistente. <p>Nota: Las licencias de alquiler (<span class="codeph"> rightsType=Rental</span>) DEBEN ser persistentes. </p> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> Clave de cifrado de clave (KEK). Las claves se almacenan cifradas con un KEK mediante un algoritmo de ajuste de claves (AES Key Wrap, RFC3394). </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kid</span> </td> 
   <td>Una representación de cadena hexadecimal de 16 bytes de la clave de cifrado de contenido o una cadena <span class="codeph"> ^somestring'</span>. La longitud de la cadena seguida de '^' no puede tener buenos 64 caracteres. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> Una representación de cadena hexadecimal de la clave de contenido cifrado. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> Una representación de cadena hexadecimal de 16 bytes de la clave de codificación de contenido </td> 
   <td>Sí, a menos que se proporcione <span class="codeph"> kek</span> y <span class="codeph"> ek</span> o <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Especifica el tipo de derechos. Debe ser <span class="codeph"> BuyToPropietario</span> o <span class="codeph"> Alquiler</span>. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.periodEndTime</span> </td> 
   <td>Fecha de finalización del alquiler. Este valor DEBE tener el formato de fecha y hora ‘RFC 3339' en el formato de indicador de zona ‘Z’ ("hora Zulu") o un entero precedido de un signo '+'. <p>Si el valor es un formato de fecha y hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> , entonces representa una fecha y hora de caducidad absoluta para la licencia. Un ejemplo de fecha y hora RFC 3339 es 2006-04-14T12:01:10Z. </p> <p> Si el valor es un entero precedido por un signo '+', se toma como un número relativo de segundos desde el momento en que se emite el token. El contenido no se puede reproducir después de este tiempo. Sólo válido si <span class="codeph"> rightsType</span> es <span class="codeph"> Rental</span>. </p> </td> 
   <td>Sí, cuando <span class="codeph"> rightsType</span> es <span class="codeph"> Rental</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.playDuration</span> </td> 
   <td>Tiempo, en segundos, que el contenido se puede reproducir una vez iniciada la reproducción. Sólo válido si <span class="codeph"> rightsType</span> es Rental. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para vídeo analógico. Intervalo válido 0-999. </td> 
   <td> Sí </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> zipDigitalAudioOPL</span> </td> 
   <td> Valor entero que indica el nivel de protección de salida para el audio digital comprimido. Intervalo válido 0-999. </td> 
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
   <td>Comportamiento requerido cuando se desconoce el resultado. Valores permitidos: <span class="codeph"> Permitir</span>, <span class="codeph"> No permitir</span> o <span class="codeph"> SDOnsolamente</span> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Un valor hexadecimal de 4 bytes para indicar los indicadores de otras opciones de control de salida </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Una palabra arbitraria de 4 letras que representa un identificador de 32 bits para una extensión. El código ASCII de 8 bits de cada letra es la parte correspondiente de 8 bits del identificador. Por ejemplo, el valor de identificador 0x61626364 (hexadecimal) se escribiría ‘<span class="codeph"> abcd</span>', porque el código ASCII de ‘a' es 0x61, etc. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Una cadena con codificación base64 de la extensión. </td> 
   <td>Sí, cuando se especifica <span class="codeph"> extensionType</span> . </td> 
  </tr> 
 </tbody> 
</table>

## Respuestas {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Cuadro 11: Respuestas HTTP**

| **Código de estado HTTP** | **Descripción** | **Content-Type** | **El cuerpo de la entidad contiene** |
|---|---|---|---|
| `200 OK` | Sin errores. | `text/uri-list` | Autentificador y URL de adquisición de licencias |
| `400 Bad Request` | Argumentos no válidos | `text/html` o `application/json` | Descripción del error |
| `401 Unauthorized` | Error de autenticación | `text/html` o `application/json` | Descripción del error |
| `404 Not found` | Dirección URL incorrecta | `text/html` o `application/json` | Descripción del error |
| `50x Server Error` | Error del servidor | `text/html` o `application/json` | Descripción del error |

**Cuadro 12: Códigos de error de evento**

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
   <td> Se especificaron indicadores de control de salida no válidos: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Se debe proporcionar el token de autenticación </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td>Distintivo de autenticación no válido: &lt;details&gt; <p>Nota:  Esto puede suceder si el autenticador es incorrecto o al acceder a la API de prueba en *.test.express.com usando el autenticador de producción y viceversa. </p> <p importance="high">Nota: El SDK de Test y la Herramienta de prueba avanzada (ATT) solo funcionan con <span class="filepath"> *.test.express.com</span>, mientras que los dispositivos de producción deben utilizar <span class="filepath"> *.service.express.com</span>. </p> </td> 
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
   <td><span class="codeph"> OutputControlFlag</span> debe codificarse en 4 bytes </td> 
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
   <td> -4018 </td> 
   <td>Niño <span class="codeph"> perdido</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> No se pudo obtener la clave de contenido del servicio de almacenamiento clave </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> kid</span> debe tener 32 caracteres hexadecimales </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> El chico</span> debe tener 64 caracteres después de ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>Niño <span class="codeph"> no válido</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Clave <span class="codeph"> o</span> clave cifrada no válida </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Error de tipo de salida desconocido no válido </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> La opción PlayReady está deshabilitada para este servicio </td> 
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
   <td> Falta el valor de OPL </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>Solo se puede especificar una <span class="codeph"> clave</span> o <span class="codeph"> contentKey</span> </td> 
  </tr> 
 </tbody> 
</table>
