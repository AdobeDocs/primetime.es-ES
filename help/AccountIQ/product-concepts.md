---
title: Glosario de Account IQ
description: 'Glosario de terminologías de productos.  '
source-git-commit: 8d8aa00d693b1ca7f960a71b40053e47249c63e4
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Conceptos y glosario del producto {#glossary}

Consulte la siguiente terminología del producto y sus definiciones.

## Probabilidad de uso compartido de cuentas {#account-sharing-probability-def}

Panel de tablero con gráficos que dividen los segmentos actuales que comparten puntuaciones en categorías de rango de uso compartido Muy bajo, Bajo, Moderado, Alto y Muy alto.

## Acción {#action-def}

Un evento directo o indirecto asociado a un [Operación](#operation-def) que afecta a las características (por ejemplo, puntuación de uso compartido o número de dispositivos en uso) de un segmento de operación (o cohorte) relacionado.

## Puntuación de uso compartido agregada {#sharing-probability-level-def}

Panel de tablero con gráficos que dividen los segmentos actuales que comparten puntuaciones en categorías de rango de uso compartido Muy bajo, Bajo, Moderado, Alto y Muy alto, junto con cada categoría de porcentaje de la cantidad total de flujo para el segmento.

## AuthN {#authn-def}

Autenticación o el número de intentos de autenticación. Un intento de autenticación es el proceso por el cual un usuario sin un estado de autenticación válido actualmente se redirige a su MVPD elegido, donde se identifica a sí mismo con el MVPD, normalmente con un nombre de usuario y una contraseña.

## AuthN OK {#authn-ok-def}

Número de autenticaciones correctas. Una autenticación correcta se produce cuando un MVPD confirma la identificación de un usuario y resulta en que el usuario se redirige de nuevo a la aplicación o al sitio del programador.

## AuthZ {#authz-def}

Autorización, o el número de solicitud de autorización. Una solicitud de autorización es el proceso mediante el cual un programador solicita permiso de un MVPD a través del Adobe para comenzar a transmitir el contenido solicitado por un usuario. Por lo general, el MVPD concede la solicitud en función de los derechos de contenido asociados con la suscripción MVPD del usuario (por ejemplo, si el canal asociado con el contenido está en la suscripción del usuario). Algunas respuestas de solicitud de autorización se almacenan en caché por Adobe, lo que permite que el Adobe responda inmediatamente sin pasar la solicitud al MVPD.

## AuthZ OK {#authz-ok-def}

Número de autorizaciones correctas.

## Canal {#channel-def}

Channel, también conocido como Propiedad, es una fuente de contenido de vídeo con relación temática. Tradicionalmente representa una fuente de vídeo continua distinta y accesible numéricamente de un MVPD. El canal se asigna directamente a un canal accesible de contenido disponible para los suscriptores a través de su cuadro superior definido (STB).

## Cluster {#cluster-def}

Un clúster es una colección de ubicaciones y dispositivos. Los clústeres se crean buscando ubicaciones comunes entre dispositivos. Los dispositivos que se han visto en una ubicación común se considerarán pertenecientes al mismo clúster. Dos dispositivos pueden estar en el mismo clúster aunque no tengan ubicaciones comunes pero se puedan conectar a través de las ubicaciones de otros dispositivos.

### Clúster móvil {#mobile-cluster-def}

Un clúster que no tiene dispositivos estáticos.

### Clúster estático {#static-cluster-def}

Un clúster que tiene al menos un dispositivo estático.

## Concurrencia {#consurrency-def}

La concurrencia se define por dos (o más) flujos reproducidos al mismo tiempo o muy cerca en el tiempo, de modo que el intervalo entre ellos no se puede justificar viajando a una velocidad normal.
El uso simultáneo se calcula utilizando la velocidad máxima (millas/hora) entre dos clústeres diferentes. Se considera que un usuario tiene un uso simultáneo si tiene una velocidad buena de 124 m/h a una distancia inferior a 124 millas o si tiene una velocidad buena de 400 m/h a una distancia buena de más de 124 millas. La distancia se calcula entre ubicaciones de diferentes clústeres. Se permite el uso simultáneo en el mismo clúster.

## Dispositivo {#device-def}

Un producto de hardware de vídeo digital capaz de reproducir contenido de TV en todas partes y compatible con Adobe Pass. Por ejemplo, teléfonos inteligentes, ordenadores portátiles y de escritorio, consolas de juegos y televisores inteligentes.

## Espaciado geográfico {#geographical-span-def}

Distancia entre los puntos más alejados de un conjunto de ubicaciones.

## Granularidad {#granularity-def}

en relación con el intervalo de tiempo, el tamaño del período; como una semana o un mes.

## Índice promedio de la industria {#industry-avg-index-def}

Un valor calculado para cada uno de los índices de riesgo (cuentas, uso, total) en todos los programadores y MVPD durante el lapso de tiempo seleccionado.

## IP {#ip-def}

La dirección del protocolo de Internet asignada a un dispositivo por un proveedor de servicios de Internet. Por ejemplo, el proveedor de servicios de cable y el proveedor de servicios de celda.

## Modo de aislamiento {#isolation-mode-def}

Un tipo de análisis de uso compartido en el que la evaluación de una cuenta se limita a eventos que se produjeron directamente en los programadores del segmento seleccionado.  Normalmente, se evalúan todos los eventos de cuenta, lo que proporciona una estimación mucho más precisa del uso compartido.  Algunos datos de MVPD están estructurados de manera que solo permita el análisis del modo de aislamiento.

## Ubicación {#location-def}

Un punto único en la tierra. También se denomina geolocalización para una solicitud de reproducción específica, detectada mediante los datos Pass, con una precisión de 1000 mx1000 m (un km cuadrado).

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## Empresa de medios {#media-company-def}

Media Company es una empresa propietaria de un grupo de redes de medios.

## Métrica {#metric}

La métrica es un atributo de la cuenta del suscriptor (por ejemplo, su MVPD, los programadores y canales del contenido que transmiten, el número de dispositivos que utilizan).

## Dispositivo móvil {#mobile-device-def}

Dispositivo con alta movilidad. Por ejemplo, teléfono móvil y tableta.

## MVPD {#mvpd-def}

MVPD, también conocido como Distribuidor, es agregador, distribuidor y distribuidor del contenido de vídeo de Media Company.

## Operación {#operation-def}

La operación es un registro creado para realizar un seguimiento del efecto de un [acción](#action-def) en un segmento asociado. Un ejemplo de una acción puede ser un límite colocado en el número de flujos simultáneos permitidos para cuentas identificadas por el segmento.

## Puntuación de uso compartido general {#overall-sharing-score}

Un valor que ayuda a los usuarios a comprender la magnitud del uso compartido de contraseñas en propiedades de programador o por suscriptores de MVPD y les proporciona un sentido de urgencia para actuar en consecuencia.

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## Reproducir solicitud {#play-requests-def}

Solicitud realizada por una aplicación o sitio cliente para que el Adobe solicite un token de medios para registrar y proteger un inicio de flujo.

## Programador {#programmer-def}

Programador, también conocido como Red, es una empresa subsidiaria de una empresa (corporación) más grande que posee y gestiona uno o más canales.

## requestorID {#requestorid-def}

El ID que utiliza una empresa de medios para identificarse a sí mismos o a una filial de un MVPD.  Según la implementación del programador, esto podría asignarse a una empresa de medios, programador o canal.  El ID más común que utiliza una empresa de medios para identificarse o una filial de un MVPD.  Según la implementación del programador, esto podría asignarse a una empresa de medios, programador o canal.  Tradicionalmente, se asigna a un canal.  Con la creación de pseudocanales como MML (March Madness Live) y los movimientos técnicamente dirigidos a abordar las limitaciones de datos controladas por MVPD, requestorID está empezando a estar más asociado con Media Company.

## resourceID {#resource-id-def}

El contenido solicitado por el usuario final.  Tradicionalmente, esto ha identificado el canal asociado al contenido que el usuario ha solicitado.  Las mejoras del sistema permiten que ese ID represente programas específicos (por ejemplo, con clasificaciones específicas) y que el ID siga identificando el canal asociado.

## Índice de riesgo - Uso {#risk-index-usage}

También conocido como Uso de cuentas compartidas, es un valor calculado en función del número de solicitudes de reproducción realizadas por cada cuenta ponderada según la probabilidad de uso compartido de cada cuenta. También se conoce como Uso por Cuentas Compartidas Índice de Riesgo.

## Segmento {#segmet-def}

El segmento es un conjunto de cuentas que cumplen las condiciones definidas por el usuario y especificadas por las métricas seleccionadas (por ejemplo, &quot;usuarios de MVPD A, B, C, D o E que han visto los canales X, Y o Z&quot;).

## Nivel de uso compartido {#sharing-level-def}

También conocido como Índice de Riesgo - Cuentas o Índice de Riesgo de Cuentas Compartidas, es un valor calculado basado en un promedio de la probabilidad de uso compartido calculada para cada cuenta del conjunto de MVPD seleccionados que se ha transmitido desde uno de los Canales de Programador seleccionados durante el lapso de tiempo seleccionado.

## Dispositivo estático {#static-device-def}

Un dispositivo con muy baja movilidad. Por ejemplo, la consola de juegos, el cuadro superior y el conjunto de televisión.

## Lapso de tiempo {#time-frame-def}

También conocido como Periodo o Ranura de Tiempo, es la ventana de tiempo que contiene la actividad de solicitud de reproducción representada en la interfaz de usuario y en las tablas de principio a fin.

## Principales MVPD en el segmento {#top-mvpds-def}

Los principales MVPD (como máximo, 10) del segmento seleccionado como medida mediante el nivel de uso compartido, el uso de cuentas compartidas o la puntuación de uso compartido general.

## Tendencia {#trend-def}

La diferencia porcentual en la métrica asociada (por ejemplo, el porcentaje de solicitudes de reproducción totales) entre el periodo actual y el anterior.

## Suscriptores únicos {#unique-subscriber-def}

El número de cuentas de MVPD únicas para un periodo determinado que han interactuado con aplicaciones o sitios de TV del programador en todas partes que involucran a Adobe Pass durante un periodo determinado.  Esa interacción incluye cualquier actividad de la aplicación de programador o del sitio que resulte en una llamada a un servicio de Adobe Pass. Por ejemplo, comprobar el estado authN o authZ, autenticarse y autorizar. El número total de suscriptores únicos también incluirá el número de dispositivos únicos si el uso de Adobe TempPass por parte de un programador (es decir, vista previa gratuita) forma parte del segmento.

## Uso {#usage-defs}

### Usuario Avid {#avid-user-def}

Más de 37 solicitudes de reproducción al mes.

### Usuario poco frecuente {#infrequent-users-def}

Menos de 9 solicitudes de reproducción al mes.

### Usuario normal {#regular-user-def}

De 9 a 37 peticiones de reproducción al mes.

## Patrón de uso {#usage-patern-def}

Uno de un conjunto finito de etiquetas de categoría aplicadas a una cuenta que caracteriza mejor a los usuarios de la cuenta en términos de grupos sociales o comportamientos (por ejemplo, una familia pequeña, un viajero o viajero, uso compartido en medios sociales, etc.).

## Código postal {#zip-code-def}

El código postal de EE. UU. asociado con ubicaciones dentro de EE. UU.
