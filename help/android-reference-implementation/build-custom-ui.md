---
description: Puede crear fácilmente una interfaz de usuario personalizada basada en el marco de implementación de referencia.
seo-description: Puede crear fácilmente una interfaz de usuario personalizada basada en el marco de implementación de referencia.
seo-title: Creación de una interfaz de usuario personalizada
title: Creación de una interfaz de usuario personalizada
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Creación de una interfaz de usuario personalizada {#build-a-custom-user-interface}

Puede crear una interfaz de usuario personalizada basada en el marco de implementación de referencia.

Los componentes de interfaz de usuario de las siguientes funciones ya están integrados:

* Publicidades en las que se puede hacer clic
* Superposiciones de publicidad
* Enlace tardío de audio
* Subtítulos opcionales
* Escuchadores de todos los componentes anteriores

1. Edite el [!DNL PlayerFragment.java] archivo para inicializar los componentes de la interfaz de usuario que desee utilizar en el reproductor.

1. Edite el [!DNL res/player/player_fragment.xml] archivo para personalizar la interfaz de usuario.
1. Cree el proyecto.

>[!NOTE]
>
>Para realizar cambios en la interfaz de usuario en la barra de búsqueda, puede editar la clase MarkableSeekBar. La clase [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) controla el control deslizante, el control del deslizador, el marcador de anuncios, los marcadores de señal, el rango de búfer y los fondos del rango de búsqueda.