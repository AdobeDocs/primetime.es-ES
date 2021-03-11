---
description: Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.
title: Rotación clave
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Rotación de clave{#key-rotation}

Las siguientes opciones de cifrado se seleccionan en el momento del empaquetado y no se pueden modificar durante la adquisición de la licencia.

Durante el empaquetado, normalmente el contenido se cifra mediante la clave de cifrado de contenido (CEK) y el cliente obtiene una licencia que contiene el CEK para consumir el contenido. Cuando se habilita la rotación de claves, se utiliza la Clave de rotación para cifrar el contenido y la clave se puede cambiar para que cada Clave de rotación solo se utilice para cifrar una parte del contenido. Las claves de rotación están protegidas con la clave de codificación de contenido y el cliente sigue obteniendo una licencia única que contenga el CEK para consumir el contenido. La implementación del empaquetador puede controlar la clave de cifrado de contenido y las claves de rotación utilizadas, así como la frecuencia con la que cambian las claves de rotación.

El contenido empaquetado mediante la rotación de claves solo se puede reproducir en los clientes de acceso a Adobe versión 3.0 y posteriores. Los clientes más antiguos necesitarían actualizar para reproducir este contenido.
