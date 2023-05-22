---
description: Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el paso siguiente.
title: Falta conmutación por error de lista de reproducción
exl-id: aab2dde3-aee2-4ade-b8f9-91c72df0c747
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Falta conmutación por error de lista de reproducción{#missing-playlist-failover}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el paso siguiente.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, TVSDK busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si TVSDK no encuentra la misma lista de reproducción de resolución, intentará navegar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits más baja y sus variantes se agotan en el intento de encontrar una lista de reproducción válida, TVSDK irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

Su aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el `STATE_CHANGED` y la llamada de retorno correspondiente es el evento `onStateChanged` método. Este es un código que monitoriza si el reproductor cambia su estado interno a ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Para obtener más información, consulte la [!DNL PlayerFragment.java] en su SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

Si la red del lado del cliente está caída, puede utilizar este código para verificarla.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

La API proporcionará la dirección URL que se utiliza para comprobar si la red del lado del cliente está caída. Debe ser una URL válida, que devuelva el código de respuesta http 200 en solicitudes http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Si setNetworkDownVerificationUrl no está establecido, TVSDK utiliza la dirección URL MainManifest de forma predeterminada para determinar si la red está inactiva.
