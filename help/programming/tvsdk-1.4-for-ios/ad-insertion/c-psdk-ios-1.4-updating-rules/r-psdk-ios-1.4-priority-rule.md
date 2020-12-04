---
description: La regla de prioridad define el orden de prioridad de los elementos creativos de publicidad que se seleccionarán para la reproducción desde una respuesta VAST/VMAP.
keywords: priority rule;creative selection rules
seo-description: La regla de prioridad define el orden de prioridad de los elementos creativos de publicidad que se seleccionarán para la reproducción desde una respuesta VAST/VMAP.
seo-title: Reglas de prioridad
title: Reglas de prioridad
uuid: a0924b3e-45cb-45ca-8a98-ed7d42aaed14
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Reglas de prioridad{#priority-rules}

La regla de prioridad define el orden de prioridad de los elementos creativos de publicidad que se seleccionarán para la reproducción desde una respuesta VAST/VMAP.

## Una regla de prioridad tiene los atributos y valores posibles siguientes:

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
   <td><span class="codeph"> prioridad</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> Matriz de tipos MIME en minúsculas que define la prioridad en la que se deben seleccionar los elementos creativos de origen para la reproducción.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Actualmente solo se admite <span class="codeph"> host</span>. Este atributo debe estar presente cuando se definan atributos <span class="codeph"> coincidencias</span> y <span class="codeph"> valores</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> múltiple</span></td> 
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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Cadena</span></td> 
   <td><span class="codeph"> prioridad</span></td> 
   <td>El valor siempre debe ser <span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> valores</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> <p>TVSDK utilizará el atributo <span class="codeph"> matches</span> en el elemento <span class="codeph"></span> del elemento creativo de origen y coincidirá con los valores definidos en esta matriz</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
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

