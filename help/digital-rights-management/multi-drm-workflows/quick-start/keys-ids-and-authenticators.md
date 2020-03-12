---
description: Para implementar DRM necesita certificados y claves particulares, incluyendo una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido tal como están almacenadas en un sistema de administración de claves.
seo-description: Para implementar DRM necesita certificados y claves particulares, incluyendo una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido tal como están almacenadas en un sistema de administración de claves.
seo-title: Teclas, ID y autenticadores
title: Teclas, ID y autenticadores
uuid: 9e5b1a64-b4e9-442f-ac15-26831aaf585d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Teclas, ID y autenticadores{#keys-ids-and-authenticators}

Para implementar DRM necesita certificados y claves particulares, incluyendo una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido tal como están almacenadas en un sistema de administración de claves.

Necesita estos elementos para empaquetar, licenciar y reproducir el contenido protegido:

## Clave de cifrado de contenido {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

La clave de cifrado de contenido (CEK) es una cadena de 16 bytes utilizada para cifrar contenido.

**¿Qué es el CEK?** - El CEK es la clave que utiliza el empaquetador para cifrar el contenido. Es una cadena con codificación hexadecimal de 16 bytes.

**¿De dónde viene el CEK?** - Usted (el proveedor de contenido) crea esta clave usted mismo, utilizando una herramienta como OpenSSL o Notepad++. Por ejemplo:

```
openssl rand 16 -hex > cek_hex_file
```

o (para Adobe Offline Packager):

1. Genere la cadena con codificación hexadecimal de 16 bytes, como se muestra arriba o con otra herramienta. Se verá así:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Abra Bloc de notas++ y pegue en la cadena hexadecimal de 16 bytes.
1. Convierta este valor de hex ASCII mediante la codificación Base64 del valor para crear su [!DNL keyfile.bin]. (Esto está cubierto en [](../../multi-drm-workflows/quick-start/package-your-content.md)).

**¿La misma clave, nombre diferente?** - Sí, puede ver el CEK mencionado por otros nombres en otros lugares, como:

* ** [!DNL [somefile].bin]** - Adobe Offline Packager hace referencia al CEK como [!DNL [somefile].bin]; p. ej., * [!DNL Keyfile.bin]* - Este es su CEK tal como lo utiliza Adobe Offline Packager, en forma de archivo en el equipo que utiliza para empaquetar contenido.

   Usted &quot;Base64&quot; su cadena hexadecimal CEK aleatoria, y guárdela como un archivo (por ejemplo, [!DNL keyfile.bin]), generalmente ubicado en el [!DNL creds] directorio debajo de [!DNL offlinepkgr/]. En el archivo de configuración de Packager (p. ej., puede llamarlo [!DNL widevine.xml] si está empaquetando para el DRM de Widevine), consulte su CEK en el archivo de configuración de la siguiente manera:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Clave** de contenido: también puede ver el CEK denominado Clave de contenido en llamadas ( `&contentKey=`), en mensajes de error, en tickets de soporte y en otra documentación.

**¿Cuándo / dónde lo utilizo?**

1. En primer lugar, debe tener el CEK disponible en la máquina en la que está haciendo el embalaje. La herramienta de empaquetado utiliza el CEK para cifrar el contenido.
1. En segundo lugar, debe almacenar el CEK en alguna forma de sistema de administración de claves (KMS), con cada CEK asociado con su propia clave [de cifrado de](../../multi-drm-workflows/glossary/glossary-cek.md)contenido. Puede crear su propio KMS o utilizar el almacenamiento [de claves de](https://www.expressplay.com/developer/key-storage/)ExpressPlay. Esto permite que su tienda (su servidor de asignación de derechos, que gestiona la asignación de derechos del cliente y el suministro de autentificador de licencia) extraiga un distintivo de licencia del cliente del KMS mediante un ID de clave en lugar del CEK real (esto es mucho más seguro).

## ID de almacenamiento de claves de cifrado de contenido {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

El ID de almacenamiento de claves de cifrado de contenido (CEKSID) identifica de forma exclusiva la clave almacenada que descifra una parte cifrada del contenido de vídeo.

**¿Qué es el CEKSID?** - CEKSID es el identificador único de una clave de cifrado de contenido (CEK). El CEK es necesario para desbloquear el contenido protegido; el CEKSID es necesario para acceder al CEK desde donde está almacenado. Cuando esté probando la configuración, puede proporcionar un CEKSID y CEK aleatorios en el momento del empaquetado, siempre y cuando utilice la misma información para las comprobaciones de licencias y reproducción.

**¿De dónde viene?** - Usted (el proveedor de contenido) puede crear este ID usted mismo o puede utilizar un servicio como el Almacenamiento [de claves de](https://www.expressplay.com/developer/key-storage/) ExpressPlay para generar CEKSID para cada uno de sus CEK (y almacenar ambos). Además, puede utilizar CEKSID generados aleatoriamente o un esquema que se adapte a su modelo comercial. Por ejemplo, puede utilizar CEKSID que sean cadenas significativas en lugar de cadenas hexadecimales aleatorias (el nombre del ID podría consistir en temas, fechas, horas, etc.)

**¿Cómo más se llama el CEKSID?** - A veces se denomina ID *de* contenido.

## autenticador de cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

El autenticador de cliente es una clave que se obtiene de ExpressPlay cuando se configura una cuenta de administrador allí. El autenticador se utiliza en las comunicaciones con los servidores ExpressPlay.

**¿Cuáles son los autenticadores de cliente?** - Los dos autenticadores de cliente conforman el par de ID — uno para pruebas, otro para producción — que ExpressPlay se registra por usted cuando se registra en su servicio. Siempre están disponibles en la página de administración de ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**¿Cuándo uso esto?** - Esto se incluye en todas las llamadas a los servidores ExpressPlay — por ejemplo, servidores de licencias, [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/)y otras llamadas.
