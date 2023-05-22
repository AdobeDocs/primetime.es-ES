---
title: Prueba del contenido empaquetado
description: Prueba del contenido empaquetado
copied-description: true
exl-id: 98456bf8-5d4d-47a7-905a-e6dac1e826ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Prueba del contenido empaquetado {#test-the-packaged-content}

Debe comprobar que la operación de empaquetado se ha realizado correctamente mediante el Reproductor de escritorio de Adobe Primetime disponible públicamente (mediante Flash Player). Este reproductor solo admite contenido HDS. Para probar el contenido de HLS, se requiere un reproductor habilitado para TVSDK del explorador de Primetime.

1. Aloje el contenido en un servidor web.
1. Inicie el reproductor DRM de Primetime (anteriormente denominado Acceso de Adobe) en https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Pegue la URL en el manifiesto del HDS ( [!DNL .f4m]) en el campo de navegación del reproductor y haga clic en **[!UICONTROL Play]** botón.
