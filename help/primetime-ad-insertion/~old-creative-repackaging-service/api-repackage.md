---
description: Puede utilizar la API de reempaquetado de CRS para transcodificar los elementos creativos de anuncios que no sean HLS con antelación, de modo que una versión de HLS estará disponible cuando necesite ejecutarla, eliminando el retraso de 2 a 4 minutos asociado con el reempaquetado justo a tiempo (JIT).
seo-description: Puede utilizar la API de reempaquetado de CRS para transcodificar los elementos creativos de anuncios que no sean HLS con antelación, de modo que una versión de HLS estará disponible cuando necesite ejecutarla, eliminando el retraso de 2 a 4 minutos asociado con el reempaquetado justo a tiempo (JIT).
seo-title: API de reempaquetado
title: API de reempaquetado
uuid: 03cd2428-510a-4b99-8496-059a48d5abba
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---


# Reempaquetar API {#repackaging-api}

Puede utilizar la API de reempaquetado de CRS para transcodificar los elementos creativos de anuncios que no sean HLS con antelación, de modo que una versión de HLS estará disponible cuando necesite ejecutarla, eliminando el retraso de 2 a 4 minutos asociado con el reempaquetado justo a tiempo (JIT).

## Solicitud HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Envíe un comando de POST HTTP a la dirección URL especificada para indicar a CRS qué elemento creativo de publicidad desea transcodificar y qué opciones desea utilizar. El código de respuesta informa del éxito o del error y otra información.

Esta solicitud requiere un nombre de usuario y una contraseña. Puede obtenerlos del administrador técnico de cuentas de Adobe. Si necesita información sobre la autenticación, póngase en contacto con su representante de habilitación de Adobe Primetime.

Para enviar una solicitud de transcodificación a CRS, envíe un mensaje HTTP de la siguiente manera:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Método -** `POST`

* **Auth -** `Digest`

* **Encabezado -** `Content-Type: text/xml`

* **Body -** XML como en el ejemplo siguiente:

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

El bloque `RepackageList` del Cuerpo puede contener de 1 a 300 bloques `Repackage`. Si el número de bloques `Repackage` en el cuerpo supera los 300, la solicitud HTTP generará el siguiente error:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


Los parámetros opcionales y requeridos en un bloque `Repackage` son los siguientes:

* **`AdSystem`** (Requerido): El servidor de publicidad de origen, por ejemplo,  `Auditude`,  `FreeWheel`,  `Apad.tv`. Es un valor de cadena que corresponde al elemento VAST `AdSystem`.

* **`AdId`** (Requerido): es un identificador para el servidor de publicidad de terceros especificado en la solicitud. Corresponde al atributo `id` del elemento `Ad` en una respuesta VAST.

* **`CreativeURL`** (Requerido): la ubicación (URI) del elemento creativo de la publicidad que se va a transcodificar. Esto corresponde al elemento VAST `MediaFile`.

* `CreativeID` (opcional): identificador del elemento creativo de publicidad que se incluirá como parte de la experiencia de publicidad.
* **`Zone`** (Requerido): Id. de zona de su cuenta (consulte con el administrador técnico de su cuenta). Es un valor numérico que corresponde al ajuste de plataforma de Auditude `publisher_site_id`.

* **`Format`** (opcional) - Parámetros para controlar la forma en que CRS transcodifica el elemento creativo de la publicidad:

   * `clientside` - Genere resultados compatibles con la URL que utiliza TVSDK para comunicarse con la CDN.
   >[!IMPORTANT]
   >
   >Debe proporcionar este parámetro si desea que la publicidad reempaquetada sea compatible con el Ad Insertion del cliente. Si no lo proporciona, la publicidad reempaquetada solo será compatible con el Ad Insertion del lado del servidor.

   * `hls` - Genere un elemento creativo de anuncios transcodificados compatible con HLS.
   * `dash` - Genere un elemento creativo de anuncios transcodificados y compatibles con DASH.
   * `id3` - Inyecte las etiquetas de metadatos temporizados ID3 en el elemento creativo de publicidad transcodificado.
   * `targetdur` - Duración del segmento (en segundos) para el elemento creativo de anuncio transcodificado. El valor predeterminado es `targetdur=4`. Este valor debe corresponder al valor especificado en el manifiesto para `<s>` en la etiqueta de duración de destinatario: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Los recursos compatibles con DASH no son compatibles con la inserción de anuncios de Adobe Primetime.

>[!IMPORTANT]
>
>Para garantizar una reproducción más fluida, establezca `targetdur` para que coincida con la duración del fragmento de contenido.

## Respuesta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS responde a la solicitud con uno de los siguientes códigos de estado:

* **HTTP 202** : aceptado (con cuerpo vacío). Esto indica el éxito. CRS carga la publicidad transcodificada en el servidor CDN.
* **HTTP 400** : solicitud incorrecta. El XML publicado no es válido.
* **HTTP 500** : error interno del servidor. El servidor encontró un problema interno (por ejemplo, el servidor no pudo conectarse a una base de datos).

## Pretranscodificación de recursos para SSAI o CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Mediante la API de reempaquetado, puede precodificar futuros eventos SSAI o CSAI. Si los recursos están destinados a utilizarse con SSAI en el futuro, asegúrese de que todos los parámetros de las llamadas de POST son únicos. Los parámetros son: AdSystem, AdId, CreativeURL, Zona, Formato. Cualquier diferencia en este conjunto de parámetros resulta en una nueva solicitud de transcodificación para SSAI.

Para los recursos que se utilicen con CSAI en el futuro, la exclusividad de los recursos depende de Zone y CreativeURL. AdSystem y AdId no dan como resultado distintos recursos transcodificados y están disponibles para los clientes.
