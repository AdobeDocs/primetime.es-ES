---
description: La regla de prioridad define el orden de prioridad de los creativos de la publicidad que se seleccionarán para la reproducción a partir de una respuesta VAST/VMAP.
keywords: regla de prioridad;reglas de selección creativa
title: Reglas de prioridad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Reglas de prioridad {#priority-rules}

La regla de prioridad define el orden de prioridad de los creativos de la publicidad que se seleccionarán para la reproducción a partir de una respuesta VAST/VMAP.

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>Clave</b></th> 
   <th class="entry"><b>Tipo</b></th> 
   <th class="entry"><b>Valores</b></th> 
   <th class="entry"><b>Descripción</b></th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> priority</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> Una matriz de tipos MIME en minúsculas que definen la prioridad con la que se deben seleccionar los creativos de origen para la reproducción.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> artículo</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Solo actualmente <span class="codeph"> host</span> es compatible. Este atributo debe estar presente cuando <span class="codeph"> matches</span> y <span class="codeph"> values</span> atributos están definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> múltiple</span></td> 
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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> priority</span></td> 
   <td>El valor siempre debe ser <span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> <p>TVSDK utilizará el <span class="codeph"> matches</span> en el <span class="codeph"> artículo</span> del creativo de origen y hacer coincidir con los valores definidos en esta matriz</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> flujo</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td></td> 
   <td> <p>El valor puede ser <span class="codeph"> vod</span> o <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```
