---
description: Preguntas frecuentes sobre el uso de la protección de salida basada en la resolución.
title: Preguntas frecuentes sobre RBOP
exl-id: 16b95db4-43a9-4458-b7f4-94033a36542e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Preguntas frecuentes sobre RBOP {#rbop-faq}

Preguntas frecuentes sobre el uso de la protección de salida basada en la resolución.

* **P.** *Al definir un requisito de salida digital para una restricción de píxeles, se producen errores de análisis/formato al dejar de lado la versión de HDCP, pero no tengo ningún requisito de HDCP. ¿Cómo debo configurar mi requisito de salida digital en este caso?* **A.** Dado que la comprobación de la versión de HDCP no es compatible actualmente con el cliente, Adobe recomienda establecer la versión de HDCP en `1.0`. Esto garantizará que la configuración tenga el formato correcto y sea semánticamente coherente en el futuro cuando se admita la comprobación de versiones de HDCP. El siguiente fragmento ilustra una configuración con este valor HDCP.

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

* **P.** *¿Las restricciones de píxeles RBOP son discretas o se basan en intervalos?* **A.** Las restricciones de píxeles RBOP se basan en rangos. Cada recuento de píxeles define los requisitos para todos los recuentos de píxeles inferiores o iguales al recuento dado o hasta el recuento más grande menor que ese valor si existe más de una restricción de píxeles. En pocas palabras, los valores se aplican como umbrales máximos para cada recuento de píxeles verticales.

   Supongamos que se pasa a su reproductor un flujo MBR con resoluciones verticales de 240, 480, 600, 720 y 1080 con la siguiente configuración RBOP.

   **Configuración de directiva RBOP:**

   * 720P: se requiere HDCP
   * 480P: sin OP

   Se aplicarán las siguientes reglas a cada variante.

   **Transmisiones:**

   * 240, 480: Ambos son &lt;= 480; no se requerirá OP y los flujos se cargarán con o sin HDCP presente.
   * 600, 720: Ambos son &lt;= 720; se requiere HDCP para la reproducción
   * 1080: > 720; la secuencia está en la lista de bloqueados (error devuelto), ya que no se encuentra en las reglas anteriores.


* **P.** En algunos de mis dispositivos Android, las restricciones de recuento de píxeles que he definido no se aplican exactamente como están definidas. ¿Qué está pasando?

   **A.** Algunos dispositivos Android informan de que el tamaño de los fotogramas es ligeramente superior al tamaño normal. Para solucionar esta situación, ajuste el tamaño de los marcos ( `maxPixel` y `pixelCount` configuración) 20 píxeles hacia arriba. Por ejemplo, ajuste la configuración del tamaño del marco hacia arriba, desde:

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

   hasta:

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

   en, para todas las instancias de `maxPixel` y `pixelCount`.
