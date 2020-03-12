---
description: Esta sección presenta una configuración de muestra que ilustra los conceptos y la forma de la configuración.
seo-description: Esta sección presenta una configuración de muestra que ilustra los conceptos y la forma de la configuración.
seo-title: Ejemplo de configuración RBOP
title: Ejemplo de configuración RBOP
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Ejemplo de configuración RBOP {#sample-rbop-configuration}

Esta sección presenta una configuración de muestra que ilustra los conceptos y la forma de la configuración.

La siguiente configuración JSON de ejemplo define una directiva de salida de píxeles que especifica lo siguiente:

* Restringir el descifrado del vídeo a resoluciones de 1080 o inferiores
* Imponer restricciones específicas a las resoluciones de 720 y 480:

   * Para la resolución 720: requerir HDCP para salida digital; requieren protección *Copy Generation Management System - Analog* (CGMS-A) para salida analógica.
   * Para la resolución 480: requerir HDCP para salida digital; no requieren protección para el análogo

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

Tenga en cuenta lo siguiente sobre la configuración de muestra anterior:

* Las `pixelCount` especificaciones son de un nivel inferior en la estructura JSON, dentro de la `pixelConstraints` sección.

* Dentro de cada especificación de recuento de píxeles, se especifica la protección de salida tanto para la salida digital como para la analógica.
* En las especificaciones de salida digital, se especifican las versiones de HDCP, aunque el cliente no admite actualmente versiones de HDCP. Consulte las preguntas más frecuentes para obtener más información.

