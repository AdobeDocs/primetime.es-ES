---
description: Preguntas más frecuentes sobre el uso de la protección de salida basada en resolución.
seo-description: Preguntas más frecuentes sobre el uso de la protección de salida basada en resolución.
seo-title: Preguntas más frecuentes sobre RBOP
title: Preguntas más frecuentes sobre RBOP
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: fa9e89dd63c8b4c9d6eee78258957cfd30c29088
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Preguntas más frecuentes sobre RBOP {#rbop-faq}

Preguntas más frecuentes sobre el uso de la protección de salida basada en resolución.

* **P.** *Al definir un requisito de salida digital para una restricción de píxeles, se producen errores de análisis/formato al dejar la versión HDCP fuera, pero no tengo ningún requisito de HDCP. ¿Cómo debo configurar mis requisitos de salida digital en este caso?* **A.** Dado que actualmente el cliente no admite la comprobación de versiones de HDCP, Adobe recomienda configurar la versión de HDCP en `1.0`. Esto garantizará que la configuración tenga el formato correcto y sea semánticamente coherente en el futuro cuando se admita la comprobación de versiones de HDCP. El siguiente fragmento ilustra una configuración con este valor HDCP.

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

* **P.** *¿Las restricciones de píxeles de RBOP son discretas o están basadas en el rango?* **A.** Las restricciones de píxeles de RBOP se clasifican según el rango. Cada recuento de píxeles define los requisitos para todos los recuentos de píxeles inferiores o iguales al recuento dado o hasta el recuento más grande menor que ese valor si existe más de una restricción de píxeles. En pocas palabras, los valores se aplican como umbrales máximos para cada recuento vertical de píxeles.

   Supongamos que se pasa a su reproductor un flujo MBR con resoluciones verticales de 240, 480, 600, 720 y 1080 con la siguiente configuración de RBOP.

   **Configuración de directiva RBOP:**

   * 720P: se requiere HDCP
   * 480P - Sin OP

   Se aplicarán las siguientes reglas a cada variante.

   **Flujos:**

   * 240, 480: Ambos son &lt;= 480; no se requerirá OP y los flujos se cargarán con o sin HDCP presente.
   * 600, 720: Ambos son &lt;= 720; Se requiere HDCP para la reproducción
   * 1080: > 720; el flujo aparece en la lista de bloques (error devuelto), ya que no se encuentra en las reglas anteriores.


* **P.** En algunos de mis dispositivos Android, las restricciones de recuento de píxeles que he definido no se aplican exactamente como se define. ¿Qué está pasando?

   **A.** Algunos dispositivos Android tienen un tamaño de fotograma de sistema de informes ligeramente superior al tamaño normal. Para remediar esta situación, ajuste los tamaños de los marcos ( `maxPixel` y `pixelCount` los ajustes) hacia arriba en 20 píxeles. Por ejemplo, ajuste la configuración del tamaño del fotograma hacia arriba, desde:

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

