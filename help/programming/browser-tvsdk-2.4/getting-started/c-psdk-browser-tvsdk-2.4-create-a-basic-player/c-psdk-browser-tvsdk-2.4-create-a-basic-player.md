---
description: Para utilizar el TVSDK del explorador, debe crear y configurar un reproductor básico. Para reproducir contenido de vídeo, puede crear un reproductor básico de cualquiera de las dos formas siguientes utilizando el SDK TVSDK del explorador o el marco de interfaz de usuario.
seo-description: Para utilizar el TVSDK del explorador, debe crear y configurar un reproductor básico. Para reproducir contenido de vídeo, puede crear un reproductor básico de cualquiera de las dos formas siguientes utilizando el SDK TVSDK del explorador o el marco de interfaz de usuario.
seo-title: Reproductor básico
title: Reproductor básico
uuid: 44a27458-be12-452f-92b9-3cef79439257
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#basic-player-overview}

Para utilizar el TVSDK del explorador, debe crear y configurar un reproductor básico. Para reproducir contenido de vídeo, puede crear un reproductor básico de cualquiera de las dos formas siguientes: con el TVSDK del explorador o con el marco de la interfaz de usuario.

## Uso del TVSDK del explorador {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Utilice las API proporcionadas con el SDK de TVSDK del explorador directamente para codificar el reproductor de vídeo. El SDK le proporciona marcos y utilidades, así como un reproductor de referencia desde el que trabajar.

>[!TIP]
>
>Para ver que esto funciona en un reproductor de referencia, no especifique ningún atributo con `videoDiv`.

## Uso del marco de la interfaz de usuario {#section_AE02384CFEF64A448C108232AB62A9FF}

Este módulo se utiliza para crear instancias del reproductor, donde cada instancia está enlazada a un elemento DOM (modelo de objetos de documento) proporcionado por el llamador. Además de tener una instancia del TVSDK del explorador, cada instancia del reproductor aloja una serie de controles que conforman la interfaz de usuario para el reproductor.

La aplicación de cada control consta de dos aspectos:

* Un `HTMLElement`, que es la representación visual del componente en la pantalla
* A `Behavior`, que administra `HTMLElement` y proporciona una API para las interacciones

Los detalles sobre estos controles se proporcionan al `VideoPlayer` usuario mediante un objeto config, que se pasa al reproductor en su instancia. De forma predeterminada, cada componente forma una jerarquía de objetos, con el elemento proporcionado a la instancia del reproductor en la raíz del árbol. A medida que se crea cada componente, se agrega al DOM en la ubicación adecuada.

Cada componente tiene un nombre, que es su clave en el objeto de configuración cuando se registra el objeto. La clase CSS del elemento DOM subyacente se forma como un `vp-` prefijo que se agrega al nombre del componente.

Los componentes pueden ampliarse o reemplazarse, su configuración puede modificarse y se pueden establecer las propiedades iniciales. Esto le permite tener un control más amplio sobre las propiedades de la API, el nombre de la clase CSS y, opcionalmente, los aspectos de la implementación del componente. Estas opciones se pueden utilizar para personalizar la funcionalidad y permitir varias instancias de un componente que se puedan diseñar o configurar individualmente.

Se puede acceder a todas las instancias de componente con la `.behaviors` propiedad. Las instancias se pueden habilitar y deshabilitar, y se pueden mostrar u ocultar. Pero una vez creadas las instancias, no se pueden eliminar.
