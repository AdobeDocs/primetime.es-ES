---
title: Prueba del contenido empaquetado
description: Prueba del contenido empaquetado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Prueba del contenido empaquetado {#test-the-packaged-content}

Debe comprobar que la operación de empaquetado se ha realizado correctamente mediante el Reproductor de escritorio de Adobe Primetime disponible públicamente (mediante Flash Player). Este reproductor solo admite contenido HDS. Para probar el contenido de HLS, se requiere un reproductor habilitado para TVSDK del explorador de Primetime.

1. Aloje el contenido en un servidor web.
1. Inicie el reproductor DRM de Primetime (anteriormente denominado Acceso de Adobe) en https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Pegue la URL en el manifiesto del HDS ( [!DNL .f4m]) en el campo de navegación del reproductor y haga clic en **[!UICONTROL Play]** botón.
