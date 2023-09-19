---
description: Esta sección presenta una configuración de ejemplo que ilustra los conceptos y la forma de la configuración.
title: Ejemplo de configuración de RBOP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Ejemplo de configuración de RBOP {#sample-rbop-configuration}

Esta sección presenta una configuración de ejemplo que ilustra los conceptos y la forma de la configuración.

La siguiente configuración JSON de muestra define una directiva de salida de píxeles que especifica lo siguiente:

* Restringir el descifrado del vídeo a resoluciones de 1080 o inferiores
* Imponer limitaciones específicas a las resoluciones 720 y 480:

   * Para una resolución de 720: requerir HDCP para salida digital; requerir *Sistema de gestión de la generación de copias: analógico* Protección (CGMS-A) para salida analógica.
   * Para la resolución 480: requerir HDCP para la salida digital; no requieren protección para analógico

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

* El `pixelCount` Las especificaciones de están un nivel por debajo en la estructura JSON, dentro de la `pixelConstraints` sección.

* Dentro de cada especificación de recuento de píxeles, la protección de salida se especifica tanto para la salida digital como para la analógica.
* En las especificaciones de salida digital, se especifican versiones de HDCP, aunque el cliente no admite actualmente el control de versiones de HDCP. Consulte las preguntas frecuentes para obtener más información.
