---
description: 'Puede seleccionar las siguientes opciones de codificación al crear un paquete. Sin embargo, no puede modificar las opciones de cifrado durante la adquisición de licencia '
title: Rotación clave
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Rotación de clave {#key-rotation}

Puede seleccionar las siguientes opciones de codificación al crear un paquete. Sin embargo, no puede modificar las opciones de cifrado durante la adquisición de licencia:

Durante el empaquetado, el contenido suele cifrarse con la clave de cifrado de contenido (CEK). El cliente obtiene una licencia que contiene el CEK para consumir el contenido.

Cuando se habilita la rotación de claves, se utiliza la Clave de rotación para cifrar el contenido y la clave se puede cambiar para que cada Clave de rotación solo se utilice para cifrar una parte del contenido. Las claves de rotación están protegidas con la clave de codificación de contenido y el cliente sigue obteniendo una licencia única que contenga el CEK para consumir el contenido.

La implementación del empaquetador puede controlar la clave de cifrado de contenido y las claves de rotación utilizadas, así como la frecuencia con la que cambian las claves de rotación.

>[!NOTE]
>
>El contenido empaquetado mediante la rotación de claves solo se puede reproducir en clientes de Primetime DRM versión 3.0 o posterior. Es posible que los clientes más antiguos necesiten actualizar para reproducir este contenido.