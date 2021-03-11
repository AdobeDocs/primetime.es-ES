---
description: La regla de normalización define una transformación de URL que se aplicará a una URL creativa de origen obtenida de una respuesta VAST/VMAP.
keywords: normalizar regla;reglas de selección creativa
title: Normalizar reglas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Normalizar reglas{#normalize-rules}

La regla de normalización define una transformación de URL que se aplicará a una URL creativa de origen obtenida de una respuesta VAST/VMAP.

**Tabla 2: La regla de normalización tiene los siguientes atributos y valores posibles:**

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
   <td>Actualmente solo se admite <span class="codeph"> host</span>. Este atributo debe estar presente cuando <span class="codeph"> coincide con</span> y los atributos <span class="codeph"> </span> están definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>Valores posibles:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  - es igual que</li> 
     <li><span class="codeph"> ne</span> : no es igual a</li> 
     <li><span class="codeph"> co</span> - contiene</li> 
     <li><span class="codeph"> nc</span> : no contiene</li> 
     <li><span class="codeph"> sw</span> : comienza con</li> 
     <li><span class="codeph"> ew</span> : termina con</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td>TVSDK utilizará el atributo <span class="codeph"> coincide con</span> en el elemento <span class="codeph"></span> del creativo de origen y coincidirá con los valores definidos en esta matriz.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Expresión regular que se aplicará en la URL creativa de origen para que coincida.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Expresión regular que se aplicará en la URL creativa de origen a reemplazar en función de la coincidencia.</td> 
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

