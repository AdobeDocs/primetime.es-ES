---
title: API de informe
description: API de informe de audiencia
source-git-commit: 7f958c83a4dd481221feb4a266440b920ac7d195
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# API de informe {#report-api}

La interfaz de usuario tiene funciones administradas para los clientes y para el equipo de habilitación (Adobe). Los clientes pueden acceder al portal y luego crear y editar sus configuraciones. También pueden ver los informes de las impresiones de sus publicidades en la interfaz de usuario.

Las API funcionan entre bastidores para facilitar a los clientes y administradores la comunicación con la infraestructura back-end.

## Punto de conexión de API {#report-api-endpoint}

### Producción {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Parámetros de consulta


| Nombre | Importancia | Tipo de valor | ¿Obligatorio? | Valor predeterminado | Restricciones | Ejemplo/ Valores de muestra válidos |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Fecha de finalización de los datos del informe | date | Y | NINGUNO | no es más reciente que ayer en UTC-8 | ######## |
| filtros | filtrar por una o más columnas | string | N | NINGUNO | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | Cuando metaData se establece en &#39;true&#39; en la solicitud, también puede filtrar por nombre. |  |
|  |  |  |  |  |  | Las claves de filtro múltiple están separadas por punto y coma. |
|  |  |  |  |  |  | Utilice valores separados por comas para proporcionar una lista de valores para la clave de filtro |
| groupBy | Agrupe por tiempo ( año \| mes \| día) o ad_config_id. Adconfig es sinónimo de AdRule. | string | N | NINGUNO | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | Para groupBy a tiempo, proporcione uno de y o m o d |
|  |  |  |  |  |  |  |



## Encabezados {#headers}

| Nombre | Tipo de valor | Obligatorio | Valor de muestra | Importancia |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Accept | string | Y | text/csv para CSV | Tipo de respuesta esperada de la API |
|  |  |  | application/json o &#39;*/*&#39; para JSON |  |
| Token de autorización | string | Y | xyz | token de autorización |
| x-api-key | string | Y | xyz | Clave de API |
| x-gw-ims-org-id | string | Y | xyz12345 | Identificador de organización de IMS de su cuenta |

* Puede generar el token de autorización (también conocido como token de acceso) siguiendo los pasos detallados en la página de ayuda de autenticación JWT de Adobe.io.
   >[!NOTE]
   >El token de autorización tiene una caducidad de 24 horas, por lo que si utiliza la API de informes con un script recurrente, asegúrese de generar el token de autenticación antes de su caducidad o cuando aparezca un error de Oauth sobre que el token no es válido.

* Para establecer los valores correctos en el encabezado de la solicitud y generar el token de autorización (mediante autenticación JWT), deberá conocer las siguientes configuraciones para su cuenta. Póngase en contacto con el equipo de asistencia de Primetime para obtener estos valores.
ID de cuenta técnica

   * ID de organización
   * Api_key
   * Client_secret

## Salida {#output}

El resultado de la consulta de la API de informes de forma predeterminada está en formato JSON, que especifica impresiones respecto a los diferentes valores de las dimensiones (grupo por parámetro) solicitados. A continuación se muestra el resultado de muestra:

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## Códigos de error y cadenas {#error-codes-strings}

### Formato de respuesta de error {#error-response-format}

Error al procesar el &quot;código&quot; de la macro: Valor no válido especificado para el parámetro `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

La tabla siguiente muestra los códigos de error y mensajes que la API de informe puede devolver. Para ver los errores relacionados con la capa de autorización, consulte la [documentación del código de error](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) de Adobe.io.

| Código de error | Mensaje de error |
|-----------------------|------------------------------------------|
| 4001007 | Los detalles del usuario no son válidos. |
| 4001008 | Todas las zonas no pertenecen a la misma cuenta. |
| 5001010 | Error interno. |
| 4001011 | Las fechas no se envían en el formato requerido. |
| 4001012 | Las fechas están fuera de rango. |
| 4001013 | Falta el parámetro obligatorio. |
| 4001014 | La lista de zonas está vacía para la cuenta. |
| 4001015 | Claves de filtro no válidas en la solicitud. |
| 4001016 | Opción GroupBy no válida en la solicitud. |
| 4001017 | Se proporciona un ID no válido en la solicitud |

## Ejemplos de llamadas y resultados esperados {#sample-calls-expected-results}

A continuación se muestra el comando curl para obtener recuentos de impresiones mensuales entre 2020-07-01 y 2021-06-30 mediante token de acceso:

**Ejemplo de llamada a la API de informes**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Ejemplo de llamada/caso de uso | Resultado esperado |
|---|---|
| Recuperación de informes con GET de fechas de inicio y finalización: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 encabezado: Accept = application/json. o */* | Json con los siguientes parámetros con todas las publicidades pertenecientes a esta cuenta total_impressions |
| Recuperar informe con GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y header : Accept = application/json. o */* | Json con los siguientes parámetros con todos los anuncios pertenecientes a estas fechas de cuenta (formato mm-dd-aaaa \| mm-aaaa \| aaaa) total_impressions |
| Recuperar informe con GroupBy = ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id encabezado : Accept = application/json. o */* | Json con los siguientes parámetros con todas las publicidades pertenecientes a esta cuenta ad_config_id total_impressions |
| Recuperar informe con GroupBy = d \| m \| y y la GET ad_config_id: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id encabezado : Accept = application/json. o */* | Json con los siguientes parámetros con todas las publicidades pertenecientes a esta cuenta ad_config_id date (mm-dd-aaaa \| mm-aaaa \| aaaa format) total_impressions |
| Recuperación de informes con metaData=true y groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id encabezado : Accept = application/json. o */* | Json con los siguientes parámetros con todas las publicidades pertenecientes a esta cuenta ad_config_id nombre total_impresiones |
| Recuperar informe con las GET groupBy=d \| m \| y y ad_config_id : [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,encabezado ad_config_id : Accept = application/json. o */* | Json con los siguientes parámetros con todas las publicidades pertenecientes a esta cuenta ad_config_id nombre total_impresiones fechas (formato mm-dd-aaaa \| mm-aaaa \| aaaa) |
| Buscar informe para obtener todas las filas de un intervalo de fechas determinado (con sin paginar = verdadero) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 entradas en la matriz Json devuelta |
| Recuperar informe con GET de parámetros de consulta de página válidos: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 entradas en la matriz devuelta |
| Informe de recuperación, con GET de formato csv: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 encabezado: Aceptar = texto/csv | Se devuelve la cadena CSV con el encabezado: total_impressions |
| Recuperar informe, con formato csv , y groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y encabezado : Aceptar = texto/csv | Se devuelve la cadena CSV con el encabezado: fechas total_impresiones (mm-dd-aaaa \| mm-aaaa \| formato aaaa) |
| Recuperación de informes, con formato csv , y metadatos = verdadero GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true encabezado : Aceptar = texto/csv | Se devuelve la cadena CSV con el encabezado: total_impressions |
| Recuperar informe, con formato csv , metadatos = true y groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y encabezado : Aceptar = texto/csv | Se devuelve la cadena CSV con el encabezado: fechas total_impresiones (mm-dd-aaaa \| mm-aaaa \| formato aaaa) |


## Directiva de restricción de la API de informes {#report-api-throttling-policy}

* Se permiten 5 solicitudes de API durante una ventana de 5 segundos para cada usuario.
* Si un usuario supera el límite, la respuesta se retrasa 5 segundos.
* Si un usuario realiza más de 10 llamadas dentro de una ventana de 5 segundos, empezará a ser rechazado con la respuesta &quot;429 Demasiadas solicitudes&quot;.
