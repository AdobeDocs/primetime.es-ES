---
description: Para implementar DRM necesita certificados y claves particulares, incluida una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido almacenadas en un sistema de administración de claves.
title: Claves, ID y autenticadores
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Claves, ID y autenticadores{#keys-ids-and-authenticators}

Para implementar DRM necesita certificados y claves particulares, incluida una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido almacenadas en un sistema de administración de claves.

Necesita estos elementos para empaquetar, licenciar y reproducir su contenido protegido:

## Clave de cifrado de contenido {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

La clave de cifrado de contenido (CEK) es una cadena de 16 bytes que se utiliza para cifrar contenido.

**¿Qué es el CEK?** - El CEK es la clave que utiliza su empaquetador para cifrar su contenido. Es una cadena con codificación hexadecimal de 16 bytes.

**¿De dónde viene el CEK?** - Usted (el proveedor de contenido) crea esta clave usted mismo, utilizando una herramienta como OpenSSL o Notepad++. Por ejemplo:

```
openssl rand 16 -hex > cek_hex_file
```

o (para el Adobe de paquetes sin conexión):

1. Genere la cadena con codificación hexadecimal de 16 bytes, como se muestra arriba o utilizando otra herramienta. Se parecerá a esto:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Abra Notepad++ y pegue en la cadena hexadecimal de 16 bytes.
1. Convierta este valor del ASCII hexadecimal mediante la codificación Base64 del valor para crear su [!DNL keyfile.bin]. (Esto se trata en [](../../multi-drm-workflows/quick-start/package-your-content.md)).

**La misma clave, ¿nombre diferente?** - Sí, puede ver el CEK mencionado por otros nombres en otros lugares, como:

* ** [!DNL [somefile].bin]**: El Adobe de paquetes sin conexión hace referencia al CEK como [!DNL [somefile].bin]; Por ejemplo, * [!DNL Keyfile.bin]*: este es su CEK tal como lo utiliza el Adobe de paquetes sin conexión, en forma de archivo en el equipo que utiliza para empaquetar contenido.

   Usted &quot;Base64&quot; su cadena hexadecimal CEK aleatoria y guárdela como un archivo (por ejemplo, [!DNL keyfile.bin]), normalmente ubicado en el directorio [!DNL creds] debajo de [!DNL offlinepkgr/]. En el archivo de configuración de Packager (por ejemplo, puede llamarlo [!DNL widevine.xml] si está empaquetando para el DRM de Widevine), debe hacer referencia a su CEK en el archivo de configuración de esta manera:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Clave de contenido** : también puede ver el CEK referido como clave de contenido en llamadas (  `&contentKey=`), en mensajes de error, en vales de soporte y en otra documentación.

**¿Cuándo / dónde lo utilizo?**

1. Primero, necesita tener el CEK disponible en la máquina en la que está haciendo su embalaje. La herramienta de empaquetado utiliza su CEK para cifrar su contenido.
1. En segundo lugar, debe almacenar el CEK en alguna forma de Sistema de administración de claves (KMS), con cada CEK asociado con su propia [Clave de cifrado de contenido](../../multi-drm-workflows/glossary/glossary-cek.md). Puede crear su propio KMS o utilizar [Key Storage](https://www.expressplay.com/developer/key-storage/) de ExpressPlay. Esto permite que su tienda (su servidor de autorizaciones, que gestiona los derechos del cliente y la provisión del token de licencia) extraiga un token de licencia para el cliente desde el KMS utilizando un ID de clave en lugar del CEK real (esto es mucho más seguro).

## ID de almacenamiento de clave de cifrado de contenido {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

El ID de almacenamiento de clave de cifrado de contenido (CEKSID) identifica de forma exclusiva la clave almacenada que descifra un fragmento cifrado de contenido de vídeo.

**¿Qué es el CEKSID?** - El CEKSID es el identificador único de una clave de cifrado de contenido (CEK). El CEK es necesario para desbloquear el contenido protegido; el CEKSID es necesario para acceder al CEK desde donde está almacenado. Al probar la configuración, puede proporcionar un CEKSID y CEK aleatorio en el momento del empaquetado, siempre que utilice la misma información para las comprobaciones de licencias y reproducción.

**¿De dónde viene?** - Usted (el proveedor de contenido) puede crear este ID usted mismo o puede utilizar un servicio como Key  [Storags de ](https://www.expressplay.com/developer/key-storage/) ExpressPlay para generar CEKSID para cada uno de sus CEK (y almacenar ambos). Además, puede utilizar CEKSID generados aleatoriamente o emplear un esquema que se ajuste a su modelo comercial. Por ejemplo, puede utilizar CEKSID que sean cadenas significativas en lugar de cadenas hexadecimales aleatorias (el nombre de ID podría consistir en temas, fechas, horas, etc.)

**¿Cómo se llama el CEKSID?** - A veces se denomina ID de  *contenido*.

## Autenticación de cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

El autenticador de cliente es una clave que se obtiene de ExpressPlay cuando se configura una cuenta de administrador allí. El autenticador se utiliza en comunicaciones con servidores ExpressPlay.

**¿Cuáles son los autenticadores de cliente?** - Los dos autenticadores de cliente conforman el par de ID (uno para pruebas, uno para producción) que ExpressPlay registra para usted cuando se registra con su servicio. Siempre están disponibles en su página de administración de ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**¿Cuándo utilizo esto?** - Esto se incluye en todas las llamadas a servidores ExpressPlay, por ejemplo, servidores de licencias, almacenamiento de claves  [ExpressPlay](https://www.expressplay.com/developer/key-storage/) y otras llamadas.
