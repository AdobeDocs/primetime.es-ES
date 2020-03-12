---
description: 'null'
seo-description: 'null'
seo-title: Lista negra de clientes de DRM con acceso restringido al contenido protegido
title: Lista negra de clientes de DRM con acceso restringido al contenido protegido
uuid: 38bc024e-0c5b-4c1c-8d4b-94b9e0fec67e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista negra de clientes de DRM con acceso restringido al contenido protegido {#blacklist-of-drm-clients-restricted-from-accessing-protected-content}

Esta lista negra especifica los clientes Primetime DRM que no pueden acceder al contenido protegido. Los clientes se incluyen en la lista negra según la versión y la plataforma del cliente.

Ejemplo de caso de uso: En caso de que se produzca un fallo de seguridad, se puede especificar una versión más reciente del cliente DRM Primetime como la versión mínima necesaria para la adquisición de licencias y la reproducción de contenido. El servidor de licencias comprueba que el cliente Primetime DRM que realiza la solicitud de licencia cumple los requisitos de versión antes de emitir una licencia. El cliente Primetime DRM también comprueba la versión de la licencia antes de reproducir el contenido. Esta comprobación de cliente es obligatoria en el caso de dominios en los que una licencia puede transferirse a otro equipo.

Se puede identificar una versión de cliente DRM Primetime mediante los atributos especificados en la siguiente tabla:

| **Atributo** | **Valores admitidos** | **Criterios de coincidencia** | **Descripción** |
|---|---|---|---|
| Entorno | `“PC”, “PortingKit”` | Coincidencia exacta | Identifica si el cliente se está ejecutando en un escritorio o en cualquier otro dispositivo. |
| SO | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Coincidencia exacta | Plataforma |
| Arquitectura | `“32”, “64”` | Coincidencia exacta | 32 o 64 bits |
| Tipo de pantalla | `“PC”, “Mobile”, “TV”` | Coincidencia exacta |  |
| Versión de tiempo de ejecución | Un número de versión válido. Por ejemplo, `“2.0.0”, "3.0", "4.0", "11.0"`, etc. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Versión de la biblioteca DRM de Primetime | Un número de versión válido. Por ejemplo, `“2.0.0”`. | Coincide si la versión del cliente es menor o igual que la versión especificada. | El número de versión se especifica como una combinación de números y puntos (&quot;.&quot;) de cualquier longitud. |
| Proveedor OEM | Cadena de proveedor OEM que puede encontrarse en el certificado de tiempo de ejecución que se emitió a un cliente que portó DRM de Primetime a un dispositivo. | Coincidencia exacta | Cadena de identificación de proveedor OEM para el dispositivo que utiliza el kit de portación. |
| Modelo | Cadena de modelo que puede encontrarse en el certificado de tiempo de ejecución que se emitió a un cliente que portó DRM de Primetime a un dispositivo. Por ejemplo, `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Coincidencia exacta | Cadena de identificación del modelo de dispositivo para el dispositivo que utiliza el kit de portación. |

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Al especificar una entrada en la lista negra, puede definir valores para uno o varios de los atributos mencionados en la tabla anterior. Cualquier atributo que no se especifique se tratará como comodín. Si el cliente DRM Primetime coincide con todos los valores especificados en una entrada de lista negra, es posible que ese cliente no tenga acceso al contenido protegido.

