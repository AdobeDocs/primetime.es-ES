---
description: Puede crear fácilmente una interfaz de usuario personalizada basada en el marco de implementación de referencia.
title: Creación de una interfaz de usuario personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Crear una interfaz de usuario personalizada {#build-a-custom-user-interface}

Puede crear una interfaz de usuario personalizada basada en el marco de implementación de referencia.

Los componentes de interfaz de usuario de las siguientes funciones ya están integrados:

* Anuncios en los que se puede hacer clic
* Superposiciones de publicidad
* Audio de enlace tardío
* Subtítulos
* Oyentes de todos los componentes anteriores

1. Edite el archivo [!DNL PlayerFragment.java] para inicializar los componentes de interfaz de usuario que desea utilizar en el reproductor.

1. Edite el archivo [!DNL res/player/player_fragment.xml] para personalizar la interfaz de usuario.
1. Cree el proyecto.

>[!NOTE]
>
>Para realizar cambios en la IU en la barra de búsqueda, puede editar la clase MarkableSeekBar . La clase [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) gestiona el control deslizante, el control del control deslizante, el marcador de anuncio, los marcadores de señal, el intervalo de búfer y los fondos del rango de búsqueda.