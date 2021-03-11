---
title: Lista de bloqueados de clientes DRM restringida del acceso a contenido protegido
description: Lista de bloqueados de clientes DRM restringida del acceso a contenido protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Lista de bloqueados de clientes DRM restringida para acceder a contenido protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Esta lista de bloqueados especifica los clientes de DRM de Primetime que no pueden acceder al contenido protegido. La lista de bloqueados de clientes se realiza según la versión del cliente y la plataforma.

Ejemplo de caso de uso: En caso de una infracción de seguridad, se puede especificar una versión más reciente del cliente de DRM de Primetime como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido. El servidor de licencias comprueba que el cliente de Primetime DRM que realiza la solicitud de licencia cumple los requisitos de versión antes de emitir una licencia. El cliente de DRM de Primetime también comprueba la versión en la licencia antes de reproducir contenido. Esta comprobación de cliente es necesaria en el caso de los dominios en los que una licencia puede transferirse a otra máquina.

Una versión de cliente de DRM de Primetime puede identificarse con los atributos especificados en la siguiente tabla:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Entorno | `“PC”, “PortingKit”` | Coincidencia exacta | Identifica si el cliente se está ejecutando en un Escritorio o en cualquier otro dispositivo. |
| Sistema operativo | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Coincidencia exacta | Plataforma |
| Arquitectura | `“32”, “64”` | Coincidencia exacta | 32 o 64 bits |
| Tipo de pantalla | `“PC”, “Mobile”, “TV”` | Coincidencia exacta |  |
| Versión de tiempo de ejecución | Un número de versión válido. Por ejemplo, `“2.0.0”, "3.0", "4.0", "11.0"`, etc. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Versión de biblioteca DRM de Primetime | Un número de versión válido. Por ejemplo, `“2.0.0”`. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Proveedor OEM | Cadena de proveedor OEM que se puede encontrar en el certificado de tiempo de ejecución emitido a un cliente que portó DRM de Primetime a un dispositivo. | Coincidencia exacta | Cadena de identificación del proveedor OEM para el dispositivo que utiliza el kit de portabilidad. |
| Modelo | Cadena de modelo que se puede encontrar en el certificado de tiempo de ejecución emitido a un cliente que portó DRM de Primetime a un dispositivo. Por ejemplo, `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Coincidencia exacta | Cadena de identificación del modelo de dispositivo para el dispositivo que utiliza el kit de portada. |

>[!NOTE]
>
>Al especificar una entrada en la lista de bloqueados, se pueden definir valores para uno o varios de los atributos mencionados en la tabla anterior. Cualquier atributo que no se especifique se trata como comodín. Si el cliente de DRM de Primetime coincide con todos los valores especificados en una entrada de lista de bloqueados, es posible que ese cliente no pueda acceder al contenido protegido.

