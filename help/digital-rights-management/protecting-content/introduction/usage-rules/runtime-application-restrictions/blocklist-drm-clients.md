---
title: Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido
description: Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Esta lista de bloqueados especifica los clientes DRM de Primetime que no pueden acceder al contenido protegido. Lista de bloqueados de clientes por versión de cliente y plataforma.

Ejemplo de caso de uso: En caso de una violación de seguridad, se puede especificar una versión más reciente del cliente DRM de Primetime como la versión mínima requerida para la adquisición de licencia y la reproducción de contenido. El servidor de licencias comprueba que el cliente DRM de Primetime que realiza la solicitud de licencia cumple los requisitos de versión antes de emitir una licencia. El cliente DRM de Primetime también comprueba la versión en la licencia antes de reproducir contenido. Esta comprobación del cliente es necesaria en el caso de los dominios en los que una licencia puede transferirse a otro equipo.

Una versión de cliente DRM de Primetime puede identificarse mediante los atributos especificados en la siguiente tabla:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Entorno | `“PC”, “PortingKit”` | Coincidencia exacta | Identifica si el cliente se está ejecutando en un escritorio o en cualquier otro dispositivo. |
| SO | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Coincidencia exacta | Plataforma |
| Arquitectura | `“32”, “64”` | Coincidencia exacta | 32 o 64 bits |
| Tipo de pantalla | `“PC”, “Mobile”, “TV”` | Coincidencia exacta | |
| Versión de tiempo de ejecución | Un número de versión válido. Por ejemplo, `“2.0.0”, "3.0", "4.0", "11.0"`, etc. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Versión de biblioteca DRM de Primetime | Un número de versión válido. Por ejemplo, `“2.0.0”`. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Proveedor OEM | Cadena de proveedor OEM que se puede encontrar en el certificado de tiempo de ejecución emitido a un cliente que transfirió Primetime DRM a un dispositivo. | Coincidencia exacta | Cadena de identificación del proveedor OEM para el dispositivo que usa el kit de portabilidad. |
| Modelo | Cadena de modelo que se puede encontrar en el certificado de tiempo de ejecución emitido a un cliente que transfirió Primetime DRM a un dispositivo. Por ejemplo, `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Coincidencia exacta | Cadena de identificación del modelo del dispositivo para el dispositivo que usa el kit de portabilidad. |

>[!NOTE]
>
>Al especificar una entrada en la lista de bloqueados, puede definir valores para uno o varios de los atributos mencionados en la tabla anterior. Cualquier atributo no especificado se trata como comodín. Si el cliente DRM de Primetime coincide con todos los valores especificados en una entrada de lista de bloqueados, es posible que ese cliente no acceda al contenido protegido.
