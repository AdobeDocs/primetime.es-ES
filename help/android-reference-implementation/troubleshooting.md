---
seo-title: Resolución de problemas
title: Resolución de problemas
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Resolución de problemas{#troubleshooting}

* Para algunos dispositivos antiguos que ejecutan API de nivel 10 o superior, logcat no puede abrir el dispositivo de registro debido a un problema de permisos. Aparece la siguiente excepción: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` Solución **alternativa:**

   1. Se abre [!DNL AndroidManifest.xml] debajo del [!DNL CatalogActivity] proyecto en el espacio de trabajo.

   1. Agregue el siguiente permiso al [!DNL `AndroidManfest.xml`] archivo:

      ```
      android.permission.READ_LOGS
      ```
