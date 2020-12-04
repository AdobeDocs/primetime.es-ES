---
seo-title: Lista de bloqueados de clientes de DRM restringidos para acceder a contenido protegido
title: Lista de bloqueados de clientes de DRM restringidos para acceder a contenido protegido
uuid: c05aa6f8-32d9-42aa-a9c5-0d0629d49778
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Lista de bloqueados de clientes de DRM restringidos para acceder a contenido protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Las versiones del módulo DRM de acceso a Adobe restringieron el acceso al contenido protegido.**

Especifica el cliente DRM que no puede acceder al contenido. Especificado por la versión y la plataforma del cliente DRM.

Ejemplo de caso de uso: En el evento de una infracción de seguridad, se puede especificar una versión más reciente del cliente DRM como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido. El servidor de licencias comprueba que el cliente DRM que realiza la solicitud de licencia cumple los requisitos de versión antes de emitir una licencia. El cliente DRM también comprueba la versión DRM en la licencia antes de reproducir el contenido. Esta comprobación de cliente es obligatoria en el caso de dominios en los que una licencia puede transferirse a otro equipo.

Una versión de cliente DRM puede identificarse mediante los atributos especificados en la siguiente tabla:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Entorno | &quot;PC&quot;, &quot;PortingKit&quot; | Coincidencia exacta | Identifica si el cliente se está ejecutando en un escritorio o en cualquier otro dispositivo. |
| SO | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Coincidencia exacta | Plataforma |
| Arquitectura | &quot;32&quot;, &quot;64&quot; | Coincidencia exacta | 32 o 64 bits |
| Tipo de pantalla | &quot;PC&quot;, &quot;Móvil&quot;, &quot;TV&quot; | Coincidencia exacta |  |
| Versión de tiempo de ejecución | Un número de versión válido. Por ejemplo: &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot;, etc. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Versión de la biblioteca DRM | Un número de versión válido. Por ejemplo, &quot;2.0.0&quot;. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Proveedor OEM | Cadena de proveedor OEM | Coincidencia exacta | Cadena de identificación de proveedor OEM para el dispositivo que utiliza el kit de portación. |
| Modelo | Cadena de modelo. Por ejemplo, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Coincidencia exacta | Cadena de identificación del modelo de dispositivo para el dispositivo que utiliza el kit de portación. |

>[!NOTE]
>
>Al especificar una entrada en la lista de bloqueados, se pueden definir valores para uno o varios de los atributos mencionados en la tabla anterior. Cualquier atributo que no se especifique se tratará como comodín. Si el cliente DRM coincide con todos los valores especificados en una entrada de lista de bloqueados, es posible que ese cliente no tenga acceso al contenido protegido.

