---
title: Actualización del archivo de configuración global
description: Actualización del archivo de configuración global
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Actualización del archivo de configuración global{#updating-the-global-configuration-file}

La contraseña de HSM en [!DNL flashaccess-global.xml] puede modificarse en cualquier momento y los cambios surtirán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios en los elementos &quot;Registro&quot; y &quot;Almacenamiento en caché&quot; no se vuelven a cargar; cualquier cambio en estos elementos requiere un reinicio del servidor.
