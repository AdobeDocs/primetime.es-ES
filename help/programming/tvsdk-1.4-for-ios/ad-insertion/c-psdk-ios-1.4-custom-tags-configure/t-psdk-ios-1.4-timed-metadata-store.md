---
description: La aplicación debe utilizar los objetos PTTimedMetadata adecuados en los momentos apropiados.
title: Almacenar objetos de metadatos cronometrados a medida que se envían
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Almacenar objetos de metadatos cronometrados a medida que se envían {#store-timed-metadata-objects-as-they-are-dispatched}

La aplicación debe utilizar los objetos PTTimedMetadata adecuados en los momentos apropiados.

Durante el análisis de contenido, que se produce antes de la reproducción, TVSDK identifica las etiquetas suscritas y notifica a la aplicación sobre estas etiquetas. La hora asociada a cada una `PTTimedMetadata` es el tiempo absoluto en la cronología de reproducción.

La aplicación debe completar las siguientes tareas:

1. Realizar un seguimiento del tiempo de reproducción actual.
1. Hacer coincidir el tiempo de reproducción actual con el tiempo de envío `PTTimedMetadata` objetos.

1. Utilice el `PTTimedMetadata` donde la hora de inicio es igual a la hora de reproducción actual.

   >[!NOTE]
   >
   >El siguiente código supone que solo hay uno `PTTimedMetadata` instancia a instancia. Si hay varias instancias, la aplicación debe guardarlas correctamente en un diccionario. Un método consiste en crear una matriz a la vez y almacenar todas las instancias en esa matriz.

   El siguiente ejemplo muestra cómo guardar `PTTimedMetadata` objetos en una `NSMutableDictionary (timedMetadataCollection)` marcado por la hora de inicio de cada `timedMetadata`.

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

## Análisis de etiquetas ID3 de Nielsen {#example_3B51E9D4AF2449FAA8E804206F873ECF}

Para extraer la etiqueta ID3 para analizarla, utilice lo siguiente en la `onMediaPlayerSubscribedTagIdentified` método:

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

Después de analizar la etiqueta ID3, extraiga los metadatos específicos de Nielsen mediante lo siguiente:

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
