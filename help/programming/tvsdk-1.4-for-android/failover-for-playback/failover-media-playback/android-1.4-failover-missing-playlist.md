---
description: Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no puede recuperarse, la aplicación determina el paso siguiente.
seo-description: Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no puede recuperarse, la aplicación determina el paso siguiente.
seo-title: Falta la conmutación por error de la lista de reproducción
title: Falta la conmutación por error de la lista de reproducción
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Falta la conmutación por error de la lista de reproducción{#missing-playlist-failover}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no puede recuperarse, la aplicación determina el paso siguiente.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, TVSDK busca una lista de reproducción variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción variante y los segmentos desde la posición coincidente. Si TVSDK no encuentra la misma lista de reproducción de resolución, intentará desplazarse por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan al intentar encontrar una lista de reproducción válida, TVSDK irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el `STATE_CHANGED` evento y la llamada de retorno correspondiente es el `onStateChanged` método. Este es un código que controla si el reproductor cambia su estado interno a ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Para obtener más información, consulte el [!DNL PlayerFragment.java] archivo en el SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

Si la red del lado del cliente está inactiva, puede utilizar este código para verificar.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

La API proporcionará la dirección URL que se utiliza para verificar si la red del lado del cliente está inactiva. Debe ser una dirección URL válida, que devuelve el código de respuesta http 200 en las solicitudes http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Si no se establece setNetworkDownVerifyUrl, TVSDK utiliza la dirección URL MainManifest de forma predeterminada para determinar si la red está inactiva.
