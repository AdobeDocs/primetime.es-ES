---
description: Para utilizar el TVSDK del explorador, debe crear y configurar un reproductor básico. Para reproducir contenido de vídeo, puede crear un reproductor básico de cualquiera de las dos formas siguientes utilizando el SDK de TVSDK del explorador o utilizando el marco de IU.
title: Reproductor básico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Información general {#basic-player-overview}

Para utilizar el TVSDK del explorador, debe crear y configurar un reproductor básico. Para reproducir contenido de vídeo, puede crear un reproductor básico de cualquiera de las dos maneras siguientes: uso del SDK TVSDK del explorador o del marco de la interfaz de usuario.

## Uso del TVSDK del explorador {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Utilice las API proporcionadas con el SDK de TVSDK del explorador directamente para codificar el reproductor de vídeo. El SDK le proporciona marcos y utilidades, así como un reproductor de referencia desde el que trabajar.

>[!TIP]
>
>Para ver que esto funciona en un reproductor de referencia, no especifique ningún atributo con `videoDiv`.

## Uso del marco de IU {#section_AE02384CFEF64A448C108232AB62A9FF}

Este módulo se utiliza para crear instancias del reproductor, donde cada instancia está enlazada a un elemento del modelo de objetos de documento (DOM) proporcionado por el llamador. Además de tener una instancia del TVSDK del explorador, cada instancia del reproductor aloja una serie de controles que conforman la interfaz de usuario del reproductor.

La aplicación de cada control consta de dos aspectos:

* Un `HTMLElement`, que es la representación visual del componente en la pantalla
* Un `Behavior`, que administra el `HTMLElement` y proporciona una API para las interacciones

Los detalles sobre estos controles se proporcionan al `VideoPlayer` mediante un objeto de configuración, que se pasa al reproductor en su instancia. De forma predeterminada, cada componente forma una jerarquía de objetos, con el elemento proporcionado a la instancia del reproductor en la raíz del árbol. A medida que se crea cada componente, se añade al DOM en la ubicación adecuada.

Cada componente tiene un nombre, que es su clave en el objeto de configuración cuando se registra el objeto. La clase CSS del elemento DOM subyacente se forma como un prefijo `vp-` que se añade al nombre del componente.

Los componentes se pueden ampliar o reemplazar, su configuración se puede modificar y se pueden establecer las propiedades iniciales. Esto le permite tener un control más amplio sobre las propiedades de la API, el nombre de la clase CSS y, opcionalmente, los aspectos de la implementación de componentes. Estas opciones se pueden utilizar para personalizar la funcionalidad y permitir varias instancias de un componente que se puedan diseñar o configurar individualmente.

Se puede acceder a todas las instancias de componentes con la propiedad `.behaviors` . Las instancias se pueden habilitar y deshabilitar, y se pueden mostrar u ocultar. Pero una vez creadas las instancias, estas no se pueden eliminar.
