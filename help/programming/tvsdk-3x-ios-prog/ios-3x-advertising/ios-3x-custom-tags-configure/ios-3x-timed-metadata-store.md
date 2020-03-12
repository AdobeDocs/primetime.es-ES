---
description: La aplicación debe utilizar los objetos PTTimedMetadata adecuados en los momentos adecuados.
seo-description: La aplicación debe utilizar los objetos PTTimedMetadata adecuados en los momentos adecuados.
seo-title: Almacenar objetos de metadatos temporizados a medida que se distribuyen
title: Almacenar objetos de metadatos temporizados a medida que se distribuyen
uuid: 38e72a9b-571a-48da-9c17-80be453e6a98
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Almacenar objetos de metadatos temporizados a medida que se distribuyen {#store-timed-metadata-objects-as-they-are-dispatched}

La aplicación debe utilizar los objetos PTTimedMetadata adecuados en los momentos adecuados.

Durante el análisis de contenido, que se realiza antes de la reproducción, TVSDK identifica las etiquetas suscritas y notifica a la aplicación sobre estas etiquetas. El tiempo que se asocia a cada uno `PTTimedMetadata` es el tiempo absoluto en la línea de tiempo de reproducción.

La aplicación debe completar las siguientes tareas:

1. Realice un seguimiento del tiempo de reproducción actual.
1. Haga coincidir el tiempo de reproducción actual con los objetos `PTTimedMetadata` enviados.

1. Utilice el `PTTimedMetadata` punto en el que la hora de inicio es igual al tiempo de reproducción actual.

   >[!NOTE]
   >
   >El código siguiente supone que solo hay una `PTTimedMetadata` instancia a la vez. Si hay varias instancias, la aplicación debe guardarlas correctamente en un diccionario. Un método consiste en crear una matriz en un momento determinado y almacenar todas las instancias de dicha matriz.

   El siguiente ejemplo muestra cómo guardar `PTTimedMetadata` objetos con una `NSMutableDictionary (timedMetadataCollection)` tecla antes de la hora de inicio de cada uno de ellos `timedMetadata`.

   ```
   NSMutableDictionary *timedMetadataCollection; 
   
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
   
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## Análisis de las etiquetas de ID3 de Nielsen {#example_3B51E9D4AF2449FAA8E804206F873ECF}

Para extraer la etiqueta ID3 para el análisis, utilice lo siguiente en el `onMediaPlayerSubscribedTagIdentified` método:

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

Después de analizar la etiqueta ID3, extraiga los metadatos específicos de Nielsen utilizando lo siguiente:

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```
