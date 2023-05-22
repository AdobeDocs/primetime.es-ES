---
description: Esta sección proporciona una descripción general conceptual de la configuración, las opciones y los significados asociados con la protección de salida.
title: Conceptos de RBOP
exl-id: 5b9de292-e060-467d-beca-5f428e45ed69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Conceptos de RBOP {#rbop-concepts}

Esta sección proporciona una descripción general conceptual de la configuración, las opciones y los significados asociados con la protección de salida.

Los requisitos de protección de salida basados en resolución se especifican en una estructura JSON jerárquica. *Los requisitos de salida se basan en píxeles.*

En el nivel más alto de la especificación JSON, puede definir la resolución de píxeles máxima y las restricciones de píxeles para resoluciones especificadas:

* `maxPixel` : la resolución de píxeles máxima define la resolución máxima con la que se producirá el descifrado.
* `pixelConstraints` : las restricciones de píxel definen los requisitos de salida que deben aplicarse para una resolución especificada.

Los requisitos de salida se asocian con restricciones de píxeles específicas. Los tipos de requisitos que se pueden asociar a una restricción de píxeles determinada incluyen restricciones para conexiones digitales, analógicas y por aire (OTA).

**Salida digital**

El requisito de salida digital puede especificar opciones restrictivas, como &quot;se requiere protección de salida digital&quot; o &quot;no se permite la reproducción&quot;. Los requisitos de salida también pueden especificar opciones menos restrictivas como &quot;no se debe aplicar ninguna protección&quot; o &quot;se debe utilizar la protección digital si está disponible&quot;.

**Salida analógica**

Las conexiones de salida analógica son más sencillas que la salida digital; consisten en un único requisito de salida.
