---
description: Puede utilizar la API de reempaquetado de CRS para transcodificar elementos creativos y no relacionados con HLS con antelación, de modo que una versión de HLS esté disponible cuando necesite ejecutarla, lo que elimina el retraso de 2 a 4 minutos asociado con el reempaquetado justo a tiempo (JIT).
title: API de reempaquetado
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# API de reempaquetado {#repackaging-api}

Puede utilizar la API de reempaquetado de CRS para transcodificar elementos creativos y no relacionados con HLS con antelación, de modo que una versión de HLS esté disponible cuando necesite ejecutarla, lo que elimina el retraso de 2 a 4 minutos asociado con el reempaquetado justo a tiempo (JIT).

## Solicitud HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Envíe un comando de POST HTTP a la dirección URL especificada para indicar a CRS qué creativo de publicidad desea transcodificar y qué opciones desea utilizar. El código de respuesta informa del éxito o el error y otra información.

Esta solicitud requiere un nombre de usuario y una contraseña. Puede obtenerlas de su administrador de cuentas técnico de Adobe. Si necesita información sobre la autenticación, póngase en contacto con su representante de habilitación de Adobe Primetime.

Para enviar una solicitud de transcodificación a CRS, envíe un mensaje HTTP como se indica a continuación:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Método -** `POST`

* **Auth -** `Digest`

* **Encabezado -** `Content-Type: text/xml`

* **Cuerpo -** XML como en el siguiente ejemplo:

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

El `RepackageList` El bloque en el cuerpo puede contener de 1 a 300 `Repackage` bloques. Si el número de `Repackage` bloques en el Body supera los 300, entonces la petición HTTP fallará con el siguiente error:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


Los parámetros obligatorios y opcionales en una `Repackage` Los bloques son los siguientes:

* **`AdSystem`** (Obligatorio): el servidor de publicidad de origen, por ejemplo, `Auditude`, `FreeWheel`, `Apad.tv`. Es un valor de cadena que corresponde al elemento VAST `AdSystem`.

* **`AdId`** (Obligatorio): Es un identificador del servidor de publicidad de terceros especificado en la solicitud. Corresponde a la variable `id` atributo del `Ad` en una respuesta VAST.

* **`CreativeURL`** (Obligatorio): La ubicación (URI) del creativo de publicidad que se va a transcodificar. Esto corresponde al VAST `MediaFile` Elemento.

* `CreativeID` (opcional): El identificador del creativo de publicidad que se va a incluir como parte de la experiencia publicitaria.
* **`Zone`** (Obligatorio): ID de zona de su cuenta (obténgalo de su administrador técnico de cuentas). Es un valor numérico que corresponde a la plataforma Auditude `publisher_site_id` configuración.

* **`Format`** (opcional): Parámetros para controlar cómo CRS transcodifica el creativo de publicidad:

   * `clientside` : genere una salida compatible con la URL que utiliza TVSDK para comunicarse con la CDN.
   >[!IMPORTANT]
   >
   >Debe proporcionar este parámetro si desea que el anuncio reempaquetado sea compatible con el Ad Insertion del lado del cliente. Si no lo proporciona, el anuncio empaquetado de nuevo solo será compatible con el Ad Insertion del lado del servidor.

   * `hls` - Generar un HLS-compatible transcodificado y creativo.
   * `dash` - Generar un DASH compatible transcodificado y creativo.
   * `id3` - Inserte etiquetas de metadatos cronometrados ID3 en el creativo y transcodificado.
   * `targetdur` - Duración del segmento (en segundos) para el anuncio transcodificado y creativo. El valor predeterminado es `targetdur=4`. Este valor debe corresponder al valor especificado en el manifiesto para `<s>` en la etiqueta de duración de target: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Los recursos compatibles con DASH no son compatibles con la inserción de anuncios de Adobe Primetime.

>[!IMPORTANT]
>
>Para garantizar una reproducción más suave, establezca `targetdur` para que coincida con la duración del fragmento de contenido.

## Respuesta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS responde a la solicitud con uno de los siguientes códigos de estado:

* **HTTP 202** - Aceptado (con cuerpo vacío). Esto indica éxito. CRS carga el anuncio transcodificado en el servidor CDN.
* **HTTP 400** - Solicitud incorrecta. El XML publicado no es válido.
* **HTTP 500** - Error interno del servidor. El servidor ha encontrado un problema interno (por ejemplo, el servidor no ha podido conectarse a una base de datos).

## Transcodificación previa de recursos para AEVM o CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Mediante la API de reempaquetado, puede pretranscodificar futuros eventos SSAI o CSAI. Si la intención es que los recursos se utilicen con SSAI en el futuro, asegúrese de que todos los parámetros de las llamadas del POST sean únicos. Los parámetros son: AdSystem, AdId, CreativeURL, Zona, Formato. Cualquier diferencia en este conjunto de parámetros resulta en una nueva solicitud de transcodificación para SAI.

Para los recursos utilizados con CSAI en el futuro, la exclusividad del recurso depende de Zone y CreativeURL. AdSystem y AdId no resultan en diferentes recursos transcodificados y estos están disponibles para los clientes.
