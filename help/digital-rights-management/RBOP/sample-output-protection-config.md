---
description: Esta sección presenta una configuración de ejemplo que ilustra los conceptos y la forma de la configuración.
title: Ejemplo de configuración RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Ejemplo de configuración de RBOP {#sample-rbop-configuration}

Esta sección presenta una configuración de ejemplo que ilustra los conceptos y la forma de la configuración.

La siguiente configuración JSON de muestra define una directiva de salida de píxeles que especifica lo siguiente:

* Restringir el descifrado del vídeo a resoluciones de 1080 o inferiores
* Imponer restricciones específicas a las resoluciones de las resoluciones 720 y 480:

   * Para la resolución 720: requerir HDCP para salida digital; requieren protección *Copy Generation Management System - Analog* (CGMS-A) para salida analógica.
   * Para la resolución 480: requerir HDCP para salida digital; no requieren protección para análogos

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

Tenga en cuenta lo siguiente sobre la configuración de ejemplo anterior:

* Las especificaciones `pixelCount` están a un nivel inferior en la estructura JSON, dentro de la sección `pixelConstraints`.

* Dentro de cada especificación de recuento de píxeles, se especifica la protección de salida tanto para la salida digital como analógica.
* En las especificaciones de salida digital, se especifican las versiones de HDCP, aunque el cliente no admite actualmente versiones de HDCP. Consulte las preguntas frecuentes para obtener más información.

