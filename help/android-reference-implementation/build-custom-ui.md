---
description: Puede crear fácilmente una interfaz de usuario personalizada basada en el marco de trabajo de implementación de referencia.
title: Crear una interfaz de usuario personalizada
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Crear una interfaz de usuario personalizada {#build-a-custom-user-interface}

Puede crear una interfaz de usuario personalizada basada en el marco de trabajo de implementación de referencia.

Los componentes de interfaz de usuario de las siguientes funciones ya están integrados:

* Anuncios en los que se puede hacer clic
* Superposiciones de anuncios
* Audio de enlace tardío
* Subtítulos opcionales
* Oyentes para todos los componentes anteriores

1. Edite el [!DNL PlayerFragment.java] para inicializar los componentes de la interfaz de usuario que desea utilizar en el reproductor.

1. Edite el [!DNL res/player/player_fragment.xml] para personalizar la interfaz de usuario.
1. Genere el proyecto.

>[!NOTE]
>
>Para realizar cambios en la interfaz de usuario de la barra de búsqueda, puede editar la clase MarkableSeekBar. El [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) La clase controla el control deslizante, el pulgar del control deslizante, el marcador de anuncio, los marcadores de referencia, el intervalo de búfer y los fondos de intervalo de búsqueda.
