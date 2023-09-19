---
title: Preparar contraseñas para los archivos de propiedades del servidor
description: Preparar contraseñas para los archivos de propiedades del servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Preparar contraseñas para los archivos de propiedades del servidor{#prepare-passwords-for-the-server-properties-files}

La implementación de referencia proporciona lo siguiente `ScrambleUtil.class`, una clase que garantiza la seguridad de la contraseña de sus credenciales.

Utilice esta herramienta para cifrar la contraseña antes de incluirla en el [!DNL flashaccess-refimpl.properties] archivo.

Para ejecutar la herramienta, puede utilizar un script Ant o Java.

La utilidad genera la contraseña cifrada, que debe copiar en el [!DNL flashaccess-refimpl.properties] archivo.

>[!NOTE]
>
>Contraseñas que se han codificado con `ScrambleUtil.class` que se ha proporcionado con la implementación de referencia no funcionan con el servidor DRM de Primetime para flujo protegido.
