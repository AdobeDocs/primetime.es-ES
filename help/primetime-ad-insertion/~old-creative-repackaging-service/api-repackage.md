---
description: Puede utilizar la API de reempaquetado de CRS para transcodificar los creativos de anuncios no HLS con antelación, de modo que haya una versión de HLS disponible cuando necesite ejecutarla, eliminando el retraso de 2-4 minutos asociado con el reempaquetado justo a tiempo (JIT).
title: API de reempaquetado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# Reempaquetado de API {#repackaging-api}

Puede utilizar la API de reempaquetado de CRS para transcodificar los creativos de anuncios no HLS con antelación, de modo que haya una versión de HLS disponible cuando necesite ejecutarla, eliminando el retraso de 2-4 minutos asociado con el reempaquetado justo a tiempo (JIT).

## Solicitud HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Envíe un comando POST HTTP a la dirección URL especificada para indicar a CRS qué creativo de publicidad desea transcodificar y qué opciones desea que utilice. El código de respuesta informa de errores o éxito y otra información.

Esta solicitud requiere un nombre de usuario y una contraseña. Puede obtenerlos del administrador técnico de cuentas de Adobe. Si necesita información sobre la autenticación, póngase en contacto con su representante de habilitación de Adobe Primetime.

Para enviar una solicitud de transcodificación a CRS, envíe un mensaje HTTP como se indica a continuación:

* **URL:** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Método -** `POST`

* **Auth -** `Digest`

* **Encabezado -** `Content-Type: text/xml`

* **Body -** XML como en el siguiente ejemplo:

   ```xml
   <RepackageList>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD1</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Zone>3</Zone>
       </Repackage>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD2</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Format>id3 targetdur=5</Format>
           <Zone>3</Zone>
       </Repackage>
   </RepackageList>
   ```

El bloque `RepackageList` del Cuerpo puede contener de 1 a 300 `Repackage` bloques. Si el número de bloques `Repackage` en el cuerpo supera los 300, la solicitud HTTP fallará con el siguiente error:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


Los parámetros opcionales y requeridos en un bloque `Repackage` son los siguientes:

* **`AdSystem`** (Obligatorio): El servidor de publicidad de origen, por ejemplo,  `Auditude`,  `FreeWheel`,  `Apad.tv`. Este es un valor de cadena que corresponde al elemento VAST `AdSystem`.

* **`AdId`** (Obligatorio): Es un identificador del servidor de publicidad de terceros especificado en la solicitud. Corresponde al atributo `id` del elemento `Ad` en una respuesta VAST.

* **`CreativeURL`** (Obligatorio) : La ubicación (URI) del creativo de publicidad que se va a transcodificar. Esto corresponde al elemento VAST `MediaFile`.

* `CreativeID` (opcional): El identificador del creativo de publicidad que se va a incluir como parte de la experiencia publicitaria.
* **`Zone`** (Obligatorio) : ID de zona de su cuenta (consulte con el administrador técnico de su cuenta). Se trata de un valor numérico que corresponde a la configuración `publisher_site_id` de la plataforma de Auditude.

* **`Format`** (opcional) - Parámetros para controlar cómo el CRS transcodifica el creativo de publicidad:

   * `clientside` - Genera resultados compatibles con la URL que utiliza TVSDK para comunicarse con la CDN.
   >[!IMPORTANT]
   >
   >Debe proporcionar este parámetro si desea que la publicidad reempaquetada sea compatible con el Ad Insertion del cliente. Si no lo proporciona, el anuncio reempaquetado solo será compatible con el Ad Insertion del servidor.

   * `hls` - Genera un creativo de anuncios transcodificados y compatible con HLS.
   * `dash` - Genera un creativo de anuncios transcodificados y compatible con DASH.
   * `id3` - Inserte etiquetas de metadatos temporizados ID3 en el creativo de publicidad transcodificado.
   * `targetdur` - Duración del segmento (en segundos) para el creativo de anuncio transcodificado. El valor predeterminado es `targetdur=4`. Este valor debe corresponder al valor especificado en el manifiesto para `<s>` en la etiqueta de duración de destino: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Los recursos compatibles con DASH no son compatibles con la inserción de anuncios de Adobe Primetime.

>[!IMPORTANT]
>
>Para garantizar una reproducción más suave, establezca `targetdur` para que coincida con la duración del fragmento de contenido.

## Respuesta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS responde a la solicitud con uno de los siguientes códigos de estado:

* **HTTP 202** : aceptado (con cuerpo vacío). Esto indica éxito. CRS carga la publicidad transcodificada en el servidor de CDN.
* **HTTP 400** : solicitud incorrecta. El XML registrado no es válido.
* **HTTP 500** : error interno del servidor. El servidor encontró un problema interno (por ejemplo, el servidor no pudo conectarse a una base de datos).

## Pretranscodificación de recursos para SSAI o CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Con la API de reempaquetado, puede pretranscodificar futuros eventos SSAI o CSAI. Si los recursos van a utilizarse con SSAI en el futuro, asegúrese de que todos los parámetros de las llamadas de POST sean únicos. Los parámetros son: AdSystem, AdId, CreativeURL, Zona, Formato. Cualquier diferencia en este conjunto de parámetros resulta en una nueva solicitud de transcodificación para SSAI.

Para los recursos utilizados con CSAI en el futuro, la exclusividad de los recursos depende de Zone y CreativeURL. AdSystem y AdId no generan recursos transcodificados diferentes y están disponibles para los clientes.
