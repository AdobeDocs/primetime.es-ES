---
description: Esta sección proporciona una descripción general conceptual de la configuración, las opciones y los significados asociados con la protección de salida.
title: Conceptos de RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Conceptos de RBOP {#rbop-concepts}

Esta sección proporciona una descripción general conceptual de la configuración, las opciones y los significados asociados con la protección de salida.

Usted especifica sus requisitos de protección de salida basados en resolución en una estructura JSON jerárquica. *Los requisitos de salida se basan en píxeles.*

En el nivel más alto de la especificación JSON, puede definir la resolución máxima de píxeles y las restricciones de píxeles para resoluciones especificadas:

* `maxPixel` - La resolución máxima de píxeles define la resolución máxima para la que se producirá el descifrado.
* `pixelConstraints` - Las restricciones de píxeles definen los requisitos de salida que deben aplicarse para una resolución especificada.

Los requisitos de salida se asocian con restricciones de píxeles específicas. Los tipos de requisitos que se pueden asociar a una restricción de píxeles determinada incluyen restricciones para conexiones digitales, analógicas y sobre el aire (OTA).

**Salida digital**

El requisito de salida digital puede especificar opciones restrictivas, como &quot;se requiere protección de salida digital&quot; o &quot;no se permite la reproducción&quot;. Los requisitos de salida también pueden especificar opciones menos restrictivas, como &quot;no se debe aplicar protección&quot; o &quot;se debe utilizar protección digital si está disponible&quot;.

**Salida analógica**

Las conexiones de salida analógicas son más sencillas que la salida digital; consisten en un único requisito de salida.
