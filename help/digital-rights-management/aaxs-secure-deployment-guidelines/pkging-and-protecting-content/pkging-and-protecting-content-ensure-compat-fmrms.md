---
title: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
description: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
copied-description: true
exl-id: 324ea561-c666-4cf9-871b-11f6b6b406f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Garantizar la compatibilidad con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x y Adobe Access usan metadatos diferentes para empaquetar contenido y solicitar licencias. Para que el acceso al Adobe utilice contenido de la versión 1.x de FMRMS, es necesario convertir los metadatos.

El SDK de acceso a Adobe admite dos opciones para convertir metadatos:

* Sin conexión (recomendado)

   Genere los metadatos de Acceso a Adobe en un proceso sin conexión y almacénelos para su uso cuando un cliente lo solicite. El Adobe recomienda esta opción. Si los metadatos se generan sin conexión, el servidor de licencias no necesita tener acceso a las CEK 1.x ni a las credenciales del empaquetador. Además, la conversión sin conexión ofrece un mejor rendimiento porque el servidor de licencias no necesita generar los metadatos en tiempo real.

* Bajo demanda

   Generar los metadatos de acceso de Adobe bajo demanda cuando un cliente lo solicite. Cuando un cliente de Acceso a Adobe descarga contenido de la versión 1.x, envía los metadatos DRM (también conocidos como encabezado DRM) al SDK de Acceso a Adobe. El SDK convierte los metadatos de DRM al formato actual. El SDK cifra e incrusta la clave de cifrado de contenido (CEK) en los metadatos y devuelve el contenido al cliente de acceso a Adobe. (Los metadatos de Adobe de Access 1.x no contienen el CEK.)

   Para convertir los metadatos, Acceso desde Adobe requiere acceso a las claves de cifrado de contenido de Adobe Access 1.x. Cuando migre de Flash Media Rights Management Server 1.x, puede seguir almacenando las claves de cifrado de contenido en la base de datos de LiveCycle ES o puede implementar una solución personalizada para almacenar de forma segura las claves de cifrado de contenido en otro lugar. Si decide seguir almacenando las claves de cifrado de contenido en la base de datos de LiveCycle ES, siga las recomendaciones descritas en &quot;Protección del acceso a contenido confidencial en la base de datos&quot; en *Endurecimiento y seguridad para el LiveCycle ES*.

Para obtener más información sobre cómo garantizar la compatibilidad con el contenido empaquetado con Flash Media Rights Management Server 1.x, consulte la *Referencia de API de acceso de Adobe*.
