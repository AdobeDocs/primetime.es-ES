---
title: Función de comprobación preliminar, cómo activar, solucionar problemas o determinar el problema
description: Función de comprobación preliminar, cómo activar, solucionar problemas o determinar el problema
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Función de comprobación previa: Cómo activar, solucionar o determinar el problema {#preflight-feature}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Se ha producido un cambio en la forma en que la autenticación de Adobe Primetime calcula preAuthorizeResources. La API de preautorización tiene una nueva implementación. Esta implementación reemplaza la solución antigua que incluye solo realizar varias llamadas de autorización.
La interfaz externa de la API PreAuthorization no cambia, no se requieren actualizaciones en la aplicación del programador.

Los recursos de Preflight se calculan de tres formas:

* **Fork y método de unión a MVPD**: esto implica que el Adobe realice múltiples llamadas de autorización a la MVPD (aunque el cliente tendrá que realizar una llamada de comprobación previa).
* **Línea de canales**: el MVPD expone la línea de canales para el usuario que ha iniciado sesión en la respuesta de autenticación SAML y el Adobe devuelve los recursos autorizados en función de eso. La respuesta SAML authN en el rastreador SAML debe exponer esa lista.
* **Autorización multicanal**: la autenticación cliente y Adobe realizan una sola llamada al MVPD para un conjunto de recursos.

Independientemente del MVPD, la aplicación cliente realizará una sola llamada al extremo Preflight (API checkPreauthorizedResources), pasando un conjunto de resourceIDs. En función de uno de los métodos anteriores admitidos por MVPD, Adobe devolverá los resourceID previamente autorizados.

Si Preflight se basa en el método fork &amp; join , el servidor de autenticación de Adobe Primetime comprueba un valor establecido para las &quot;llamadas máximas de preautorización&quot; en su configuración. Esto se configura por Adobe.

El valor predeterminado para la configuración &quot;máximo de llamadas de preautorización&quot; es &quot;5&quot;, lo que significa que solo se pueden enviar 5 recursos como máximo en Preflight para la ramificación y para unirse a los MVPD. Al pasar más de 5 recursos, se producirá una excepción y se devolverá una lista nula. Este es el comportamiento esperado. Podemos configurarlo en cualquier valor si el MVPD no admite alineación de canales o autorización de varios canales, pero solo después de consultarlos como múltiples llamadas de autorización de ramificación y de unión aumentarán sus tiempos de carga.

Por lo tanto, estas son cosas a tener en cuenta al habilitar/solucionar problemas de comprobación previa para un MVPD:

* El método que admite el MVPD (ramificación y unión, alineación de canales o multicanal).
* Si solo se admite ramificación y unión, se debe preguntar al programador cuántos ID de recurso enviará en la llamada de comprobación previa.
* El MVPD necesita ser consultado y necesita saber el impacto de hacer un número &quot;n&quot; de llamadas de autorización de ramificación y de unión. Después, el valor debe configurarse en config si es bueno a 5.

**Limitación**

Tenga en cuenta que no recuperamos ningún resourceID de la llamada de Preflight para algunos MVPD, como AT&amp;T y TWC, si alguno de los resourceID es un ID falso o un ID no reconocido en la lista de resourceID que envían en la llamada de comprobación previa, aunque también tengamos recursos válidos y autorizados en esa lista.

