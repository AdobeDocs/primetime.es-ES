---
description: Preguntas frecuentes sobre el uso de protección de salida basada en resolución.
title: Preguntas frecuentes sobre RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Preguntas frecuentes sobre RBOP {#rbop-faq}

Preguntas frecuentes sobre el uso de protección de salida basada en resolución.

* **P.** *Al definir un requisito de salida digital para una restricción de píxeles, obtengo errores de análisis/formato cuando dejo la versión HDCP fuera, pero no tengo ningún requisito de HDCP. ¿Cómo debo configurar mi requisito de salida digital en este caso?* **R.** Dado que la comprobación de versiones de HDCP no es compatible con el cliente actual, Adobe recomienda configurar la versión de HDCP en  `1.0`. Esto garantizará que la configuración tenga el formato correcto y que sea semánticamente coherente en el futuro cuando se admita la comprobación de versiones de HDCP. El siguiente fragmento ilustra una configuración con este valor HDCP.

   ```
   { "pixelConstraints":  
     [  
       { "pixelCount": 720, "digital":  
         [  
           {  
             "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
           }  
         ]  
       }  
     ]  
   }
   ```

* **P.** *¿Las restricciones de píxeles de RBOP son discretas o están basadas en rangos?* **A.** Las restricciones de píxeles de RBOP se ordenan según su rango. Cada recuento de píxeles define los requisitos para todos los recuentos de píxeles menores o iguales que el recuento dado o hasta el recuento más grande menor que ese valor si existe más de una restricción de píxeles. En pocas palabras, los valores se aplican como umbrales máximos para cada recuento de píxeles vertical.

   Supongamos que se pasa un flujo MBR con resoluciones verticales de 240, 480, 600, 720 y 1080 a su reproductor con la siguiente configuración de RBOP.

   **Configuración de directiva RBOP:**

   * 720P - Se requiere HDCP
   * 480P - Sin OP

   Se aplican las siguientes reglas a cada variante.

   **Emisiones:**

   * 240, 480: Ambos son &lt;= 480; no se requerirá OP y los flujos se cargarán con o sin HDCP presente.
   * 600, 720: Ambos son &lt;= 720; El HDCP es necesario para la reproducción
   * 1080: > 720; el flujo se incluye en la lista de bloqueados (error devuelto) ya que no se encuentra en las reglas anteriores.


* **P.** En algunos de mis dispositivos Android, las restricciones de recuento de píxeles que he definido no se aplican exactamente como se define. ¿Qué está pasando?

   **R.** Algunos dispositivos Android informan de tamaños de fotogramas ligeramente superiores al tamaño normal. Para solucionar esta situación, ajuste sus tamaños de fotograma ( `maxPixel` y `pixelCount`) hacia arriba en 20 píxeles. Por ejemplo, ajuste la configuración del tamaño del marco hacia arriba, desde:

   ```
   { 
       "maxPixel": 800, 
       "pixelConstraints": [ 
           { "pixelCount": 532, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   a:

   ```
   { 
       "maxPixel": 820, 
       "pixelConstraints": [ 
           { "pixelCount": 552, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   en todas las instancias de `maxPixel` y `pixelCount`.

