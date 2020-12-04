---
description: La regla de normalización define una transformación de URL para aplicarla a una URL creativa de origen obtenida de una respuesta VAST/VMAP.
keywords: normalize rule;creative selection rules
seo-description: La regla de normalización define una transformación de URL para aplicarla a una URL creativa de origen obtenida de una respuesta VAST/VMAP.
seo-title: Normalizar reglas
title: Normalizar reglas
uuid: ae0364d2-23e2-48d6-b9b6-869cd163080d
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# Normalizar reglas {#normalize-rules}

La regla de normalización define una transformación de URL para aplicarla a una URL creativa de origen obtenida de una respuesta VAST/VMAP.

## La regla normalizar tiene los atributos y valores posibles siguientes:

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Clave</th> 
   <th class="entry"> Tipo</th> 
   <th class="entry"> Valores</th> 
   <th class="entry"> Descripción</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> normalizar</span></td> 
   <td>El valor siempre debe ser <span class="codeph"> normalizar</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Actualmente solo se admite <span class="codeph"> host</span>. Este atributo debe estar presente cuando se definan atributos <span class="codeph"> coincidencias</span> y <span class="codeph"> valores</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>Valores posibles:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - es igual a</li> 
     <li><span class="codeph"> ne</span> - no es igual a</li> 
     <li><span class="codeph"> co</span> - contiene</li> 
     <li><span class="codeph"> nc</span> - no contiene</li> 
     <li><span class="codeph"> sw</span> : inicios con</li> 
     <li><span class="codeph"> Nuevo</span> : termina con</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> valores</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td>TVSDK utilizará el atributo <span class="codeph"> matches</span> en el elemento <span class="codeph"></span> del elemento creativo de origen y coincidirá con los valores definidos en esta matriz.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> buscar</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Una expresión normal para aplicar en la URL creativa de origen para que coincida.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> reemplazar</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Una expresión normal para aplicar en la URL creativa de origen para reemplazar según la coincidencia.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```

