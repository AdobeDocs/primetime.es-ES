---
title: Actualización del archivo de configuración global
description: Actualización del archivo de configuración global
copied-description: true
exl-id: 6544d8ae-6d23-498e-92c5-bad6bfcc10ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Actualización del archivo de configuración global{#updating-the-global-configuration-file}

La contraseña de HSM en [!DNL flashaccess-global.xml] puede modificarse en cualquier momento y los cambios surtirán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios en los elementos &quot;Registro&quot; y &quot;Almacenamiento en caché&quot; no se vuelven a cargar; cualquier cambio en estos elementos requiere un reinicio del servidor.
