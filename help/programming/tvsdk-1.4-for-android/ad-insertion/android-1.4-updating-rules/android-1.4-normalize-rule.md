---
description: La regla normalize define una transformación de URL que se aplicará a la URL creativa de origen obtenida de una respuesta VAST/VMAP.
keywords: normalizar regla;reglas de selección creativa
title: Normalizar reglas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Normalizar reglas{#normalize-rules}

La regla normalize define una transformación de URL que se aplicará a la URL creativa de origen obtenida de una respuesta VAST/VMAP.

**Tabla 2: La regla normalize tiene los siguientes atributos y valores posibles:**

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
   <td><span class="codeph"> artículo</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Solo actualmente <span class="codeph"> host</span> es compatible. Este atributo debe estar presente cuando <span class="codeph"> matches</span> y <span class="codeph"> values</span> atributos están definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>Valores posibles:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - igual a</li> 
     <li><span class="codeph"> ne</span> - no es igual a</li> 
     <li><span class="codeph"> co</span> - contiene</li> 
     <li><span class="codeph"> nc</span> - no contiene</li> 
     <li><span class="codeph"> sw</span> - empieza por</li> 
     <li><span class="codeph"> ew</span> - termina por</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td>TVSDK utilizará el <span class="codeph"> matches</span> en el <span class="codeph"> artículo</span> del creativo de origen y comparan con los valores definidos en esta matriz.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> encontrar</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Una expresión regular que se aplicará en la URL creativa de origen que corresponda.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Una expresión regular que se aplicará en la URL creativa de origen que se reemplazará en función de la coincidencia.</td> 
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
