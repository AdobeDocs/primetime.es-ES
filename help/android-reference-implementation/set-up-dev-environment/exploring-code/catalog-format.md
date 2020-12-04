---
description: La implementación de referencia Primetime utiliza un formato de fuente basado en JSON para las respuestas. Este formato se analiza mediante la implementación de la interfaz IFeedItemAdapter.
seo-description: La implementación de referencia Primetime utiliza un formato de fuente basado en JSON para las respuestas. Este formato se analiza mediante la implementación de la interfaz IFeedItemAdapter.
seo-title: Formato del catálogo
title: Formato del catálogo
uuid: 6e1a526f-c0bb-403d-a792-666caf5479a5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Formato de catálogo {#catalog-format}

La implementación de referencia Primetime utiliza un formato de fuente basado en JSON para las respuestas. Este formato se analiza mediante la implementación de la interfaz IFeedItemAdapter.

>[!NOTE]
>
>Este formato de fuente es el formato de muestra que utiliza la implementación de referencia y sirve como ejemplo de cómo se puede analizar y asignar el formato a la interfaz de fuente. Puede utilizar su propio formato de fuente de entrada con sus propias implementaciones de interfaz de fuente.

En un nivel superior, el formato consiste en una matriz de entradas de contenido. Cada entrada representa un contenido de vídeo publicado en directo o VOD:

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
| `id` | Un identificador/guía único para el contenido según lo establecido por el sistema de publicación de fuentes. |
| `title` | Un título para el contenido. |
| `description` | Descripción del contenido. |
| `categories` | Lista de categorías etiquetadas para el contenido que puede utilizar la aplicación para mejorar la experiencia del usuario. Lea las propiedades del contenido. |
| `keywords` | La aplicación puede utilizar una lista de palabras clave separadas por coma para mejorar la experiencia del usuario. Lea las propiedades del contenido. |
| `isLive` | verdadero o falso, indicando si es un flujo en directo o VOD. |
| `content` | Matriz de objetos JSON con formatos alternativos para el contenido junto con las URL correspondientes. Por ejemplo, podría haber direcciones URL para los formatos f4m y m3u8. Los atributos del objeto JSON se describen a continuación. |
| `thumbnails` | Matriz de objetos JSON con direcciones URL para diferentes tamaños de miniaturas. Los atributos del objeto JSON se definen a continuación. |
| `metadata` | Objeto JSON que define metadatos para el contenido; actualmente, estos metadatos se limitan a los metadatos relacionados con la publicidad. El objeto metadata se define a continuación. |

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
| format | Debe tener el formato m3u8 para Android. |
| url | La dirección URL del flujo de vídeo para el formato determinado. |

El siguiente bloque de código define los objetos JSON que forman la matriz de **objetos en miniatura**:

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
| format | Una cadena que indica el formato del archivo en miniatura, por ejemplo, JPEG, PNG, etc. |
| height | Altura de la miniatura. En la aplicación de referencia, la miniatura con la mayor altura y anchura se devuelve como miniatura pequeña y la que tiene la mayor anchura y altura se devuelve como miniatura grande. |
| width | Ancho de la miniatura. En la aplicación de referencia, la miniatura con la mayor altura y anchura se devuelve como miniatura pequeña y la que tiene la mayor anchura y altura se devuelve como miniatura grande. |
| url | La dirección URL del archivo de miniaturas. |

El siguiente bloque de código define el **objeto de metadatos**:

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
| ad | Metadatos relacionados con la publicidad. |
| type | El valor puede ser Publicidades Primetime, Saltos de publicidad directa o Marcadores de publicidad personalizados. <br/><br/>El PSDK proporciona compatibilidad integrada con los siguientes tipos de metadatos: Metadatos relacionados con la audiencia para Primetime Ad Serving (Primetime Ads), saltos de publicidad directos con direcciones URL de publicidad (Direct Ad Breaks) y marcadores de publicidad personalizados que proporcionan el intervalo de tiempo para cada marcador de publicidad (Custom Ad Markers). Cada tipo tiene un AdProvider integrado en el PSDK que procesa los metadatos.  <br/><br/>El formato JSON para cada uno de estos formatos se ha definido a continuación. |
| detalles | Incluye los atributos de metadatos de la publicidad. Ambos tipos de metadatos de anuncio tienen su propio conjunto de atributos definidos a continuación. Para los tipos integrados, los atributos incluidos definen los datos esperados por el PSDK para ese tipo. |
| asignación | Metadatos relacionados con la asignación de derechos |
| id | ID de recurso de medios utilizado para solicitudes de autorización en el servicio de pase de Adobe Primetime pay-TV. El ID puede ser una cadena de texto o una cadena mRSS con codificación HTML. Cualquier contenido multimedia que requiera autorización debe contener un ID de recurso válido. |

