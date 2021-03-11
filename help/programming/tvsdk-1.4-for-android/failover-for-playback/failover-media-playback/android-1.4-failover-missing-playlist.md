---
description: Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no puede recuperarse, la aplicación determina el siguiente paso.
title: Faltan errores en la lista de reproducción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Falta la conmutación por error de la lista de reproducción{#missing-playlist-failover}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no puede recuperarse, la aplicación determina el siguiente paso.

Si falta la lista de reproducción asociada a la velocidad de bits de resolución media, TVSDK busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si TVSDK no encuentra la misma lista de reproducción de resolución, tratará de pasar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan al intentar encontrar una lista de reproducción válida, TVSDK pasará a la velocidad de bits superior y contará hacia abajo desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el evento `STATE_CHANGED` y la llamada de retorno correspondiente es el método `onStateChanged`. Este es un código que controla si el reproductor cambia su estado interno a ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Para obtener más información, consulte el archivo [!DNL PlayerFragment.java] en el SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

Si la red del lado del cliente está inactiva, puede utilizar este código para verificarlo.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

La API proporcionará la url que se utiliza para verificar si la red del lado del cliente está inactiva. Debe ser una dirección url válida, que devuelve el código de respuesta http 200 en las solicitudes http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Si setNetworkDownVerifyUrl no está establecido, TVSDK utiliza la URL MainManifest de forma predeterminada para determinar si la red está inactiva.
