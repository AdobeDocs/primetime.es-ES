---
title: Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido
description: Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe Acceso a versiones del módulo DRM restringidas al acceso al contenido protegido.**

Especifica el cliente DRM que no puede acceder al contenido. Especificado por la versión y plataforma del cliente DRM.

Ejemplo de caso de uso: En caso de una brecha de seguridad, se puede especificar una versión más reciente del cliente DRM como la versión mínima requerida para la adquisición de licencia y la reproducción de contenido. El servidor de licencias comprueba que el cliente DRM que realiza la solicitud de licencia cumple los requisitos de versión antes de emitir una licencia. El cliente de DRM también comprueba la versión de DRM en la licencia antes de reproducir contenido. Esta comprobación del cliente es necesaria en el caso de los dominios en los que una licencia puede transferirse a otro equipo.

Una versión de cliente DRM puede identificarse mediante los atributos especificados en la siguiente tabla:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Entorno | &quot;PC&quot;, &quot;PortingKit&quot; | Coincidencia exacta | Identifica si el cliente se está ejecutando en un escritorio o en cualquier otro dispositivo. |
| SO | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Coincidencia exacta | Plataforma |
| Arquitectura | “32”, “64” | Coincidencia exacta | 32 o 64 bits |
| Tipo de pantalla | &quot;PC&quot;, &quot;Mobile&quot;, &quot;TV&quot; | Coincidencia exacta | |
| Versión de tiempo de ejecución | Un número de versión válido. Por ejemplo, &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot;, etc. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Versión de biblioteca DRM | Un número de versión válido. Por ejemplo, &quot;2.0.0&quot;. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Proveedor OEM | Cadena de proveedor OEM | Coincidencia exacta | Cadena de identificación del proveedor OEM para el dispositivo que usa el kit de portabilidad. |
| Modelo | Cadena de modelo. Por ejemplo, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Coincidencia exacta | Cadena de identificación del modelo del dispositivo para el dispositivo que usa el kit de portabilidad. |

>[!NOTE]
>
>Al especificar una entrada en la lista de bloqueados, se pueden definir valores para uno o varios de los atributos mencionados en la tabla anterior. Cualquier atributo no especificado se trata como comodín. Si el cliente DRM coincide con todos los valores especificados en una entrada de lista de bloqueados, es posible que dicho cliente no acceda al contenido protegido.
