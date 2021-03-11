---
title: Preparación de contraseñas para los archivos de propiedades del servidor
description: Preparación de contraseñas para los archivos de propiedades del servidor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# Preparar contraseñas para los archivos de propiedades del servidor{#prepare-passwords-for-the-server-properties-files}

La implementación de referencia proporciona `ScrambleUtil.class`, una clase que garantiza la seguridad de la contraseña de la credencial.

Utilice esta herramienta para cifrar la contraseña antes de incluirla en el archivo [!DNL flashaccess-refimpl.properties].

Para ejecutar la herramienta, puede utilizar un script Ant o Java.

La utilidad genera la contraseña cifrada, que debe copiarse en el archivo [!DNL flashaccess-refimpl.properties].

>[!NOTE]
>
>Las contraseñas que se han codificado con la `ScrambleUtil.class` que se ha proporcionado con la implementación de referencia no funcionan con el servidor de DRM de Primetime para la transmisión protegida.
