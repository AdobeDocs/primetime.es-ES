---
title: Resolución de problemas
description: Resolución de problemas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# Solución de problemas{#troubleshooting}

* Para algunos dispositivos antiguos que ejecutan API de nivel 10 o superior, logcat no puede abrir el dispositivo de registro debido a un problema de permisos. Aparece la siguiente excepción: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Solución:**

   1. Abra [!DNL AndroidManifest.xml] en el proyecto [!DNL CatalogActivity] del espacio de trabajo.

   1. Agregue el siguiente permiso al archivo [!DNL `AndroidManfest.xml`]:

      ```
      android.permission.READ_LOGS
      ```
