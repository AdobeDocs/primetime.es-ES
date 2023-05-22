---
description: La implementación de referencia de Primetime utiliza un formato de fuente basado en JSON para las respuestas. Este formato se analiza mediante una implementación de la interfaz IFeedItemAdapter.
title: Formato de catálogo
exl-id: faaeb647-9c01-4290-be1e-2b8461c8ad27
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Formato de catálogo {#catalog-format}

La implementación de referencia de Primetime utiliza un formato de fuente basado en JSON para las respuestas. Este formato se analiza mediante una implementación de la interfaz IFeedItemAdapter.

>[!NOTE]
>
>Este formato de fuente es el formato de muestra que utiliza la implementación de referencia y sirve como ejemplo de cómo se puede analizar y asignar el formato a la interfaz de fuente. Puede utilizar su propio formato de fuente de entrada con sus propias implementaciones de interfaz de fuente.

En un nivel superior, el formato consiste en una matriz de entradas de contenido. Cada entrada representa un contenido de vídeo publicado en directo o en VOD:

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

Cada entrada de fuente es un objeto JSON con un conjunto determinado de atributos:

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| Propiedad | Descripción |
|---|---|
| `id` | Un identificador o guía único para el contenido tal como lo establece el sistema de publicación de fuentes. |
| `title` | Un título para el contenido. |
| `description` | Una descripción del contenido. |
| `categories` | Una lista de categorías etiquetadas para el contenido que la aplicación puede utilizar para mejorar la experiencia del usuario. Lea las propiedades del contenido. |
| `keywords` | La aplicación puede utilizar una lista de palabras clave separadas por comas para mejorar la experiencia del usuario. Lea las propiedades del contenido. |
| `isLive` | true o false, lo que indica si se trata de una transmisión en directo o de VOD. |
| `content` | Una matriz de objetos JSON con formatos alternativos para el contenido junto con las direcciones URL correspondientes. Por ejemplo, podría haber direcciones URL para los formatos f4m y m3u8. Los atributos de objeto JSON se describen más adelante. |
| `thumbnails` | Matriz de objetos JSON con direcciones URL para diferentes tamaños de miniaturas. A continuación se definen los atributos del objeto JSON. |
| `metadata` | Objeto JSON que define metadatos para el contenido. Actualmente, estos metadatos se limitan a metadatos relacionados con anuncios. El objeto de metadatos se define a continuación. |

El siguiente bloque de código define los objetos JSON que forman la matriz de **objetos de contenido**:

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| Propiedad | Descripción |
|--- |--- |
| formato | Debe tener el formato m3u8 para Android. |
| url | La URL del flujo de vídeo para el formato dado. |

El siguiente bloque de código define los objetos JSON que forman la matriz de **objetos de miniatura**:

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| Propiedad | Descripción |
|---|---|
| formato | Una cadena que indica el formato del archivo de miniaturas, por ejemplo, JPEG, PNG, etc. |
| altura | Altura de la miniatura. En la aplicación de referencia, la miniatura con la altura y anchura más pequeñas se devuelve como la miniatura pequeña, y la que tiene la anchura y altura más grandes se devuelve como la miniatura grande. |
| anchura | Ancho de la miniatura. En la aplicación de referencia, la miniatura con la altura y anchura más pequeñas se devuelve como la miniatura pequeña, y la que tiene la anchura y altura más grandes se devuelve como la miniatura grande. |
| url | La URL del archivo de miniaturas. |

El siguiente bloque de código define la variable **objeto de metadatos**:

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| Propiedad | Descripción |
|--- |--- |
| anuncio | Metadatos relacionados con el anuncio. |
| type | El valor puede ser Anuncios de Primetime, Pausas publicitarias directas o Marcadores de publicidad personalizados. <br/><br/>El PSDK proporciona compatibilidad integrada con los siguientes tipos de metadatos: metadatos relacionados con la audiencia para el servicio de publicidad de Primetime (anuncios de Primetime), pausas publicitarias directas con direcciones URL (pausas publicitarias directas) y marcadores de publicidad personalizados que proporcionan el intervalo de tiempo para cada marcador de publicidad (marcadores de publicidad personalizados). Cada tipo tiene un AdProvider integrado en el PSDK que procesa los metadatos.  <br/><br/>A continuación se define el formato JSON para cada uno de ellos. |
| detalles | Incluye los atributos de metadatos de publicidad. Ambos tipos de metadatos de publicidad tienen su propio conjunto de atributos definidos a continuación. Para los tipos integrados, los atributos incluidos definen los datos esperados por el PSDK para ese tipo. |
| derecho | Metadatos relacionados con derechos |
| id | ID de recurso de medios utilizado para las solicitudes de autorización contra el servicio de pase de televisión de pago de Adobe Primetime. El ID puede ser una cadena de texto o una cadena mRSS con codificación de HTML. Cualquier contenido multimedia que requiera autorización debe contener un ID de recurso válido. |
