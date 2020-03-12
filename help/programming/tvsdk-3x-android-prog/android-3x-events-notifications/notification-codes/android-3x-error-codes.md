---
title: Códigos de error de PSDK
description: Información sobre varios códigos de error, advertencias y códigos de error nativos.
translation-type: tm+mt
source-git-commit: eddc327087411a6214cfd8dafef66b850a603f97

---


# Códigos de error de PSDK {#psdk-error-codes}

Continúe leyendo para conocer los códigos de error, las advertencias y los códigos de error nativos de PSDK.

## Errores

La siguiente tabla proporciona información detallada sobre las notificaciones de tipo ERROR. La mayoría de los errores contienen metadatos pertinentes; por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1">
  <tr> 
   <th><b>Nombre de error de PSDK</b></th>
   <th><b>Código de error de PSDK</b></th>
   <th><b>Descripción</b></th>
  </tr>
  <tr>
    <td>ÉXITO</td>
    <td>0</td>
    <td>La operación realizada por la API subyacente se realiza correctamente.</td>
  </tr>
  <tr>
    <td>INVALID_ARGUMENT</td>
    <td>1</td>
    <td>Los datos o el formato del argumento proporcionados a la API subyacente no son válidos.</td>
  </tr>
  <tr>
    <td>NULL_POINTER</td>
    <td>2</td>
    <td>Uno de los argumentos pasados es NULL O uno de los miembros internos no se inicializó.</td>
  </tr>
  <tr>
    <td>ILLEGAL_STATE</td>
    <td>3</td>
    <td>La operación no se admite en el estado del reproductor actual.</td>
  </tr>
  <tr>
    <td>INTERFACE_NOT_FOUND</td>
    <td>4</td>
    <td>El método interfaceCast emite este error cuando esta interfaz solicitada no se implementa/hereda.</td>
  </tr>
  <tr>  
    <td>CREATION_FAILED</td>
    <td>5</td>
    <td>Error al crear uno de los recursos internos.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_OPERATION</td>
    <td>6</td>
    <td>La operación solicitada no se admite actualmente.</td>
  </tr>
  <tr>
    <td>DATA_NOT_AVAILABLE</td>
    <td>7</td>
    <td>Los datos solicitados no están disponibles en este momento.</td>
  </tr>
  <tr>
    <td>SEEK_ERROR</td>
    <td>8</td>
    <td>Error al realizar una operación de búsqueda.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_FEATURE</td>
    <td>9</td>
    <td>Esta función no es compatible.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>10</td>
    <td>El valor especificado está fuera de rango.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>11</td>
    <td>El códec de audio/vídeo de un flujo determinado no es compatible con TVSDK ni con el dispositivo subyacente.</td>
  </tr>
  <tr>
    <td>MEDIA_ERROR</td>
    <td>12</td>
    <td>No se encuentra el medio especificado.</td>
  </tr>
  <tr>
    <td>NETWORK_ERROR</td>
    <td>13</td>
    <td>Error al descargar un fragmento o segmento (vídeo y audio).</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>14</td>
    <td>Evento de error genérico. En realidad no es emitido por TVSDK. Solo es un marcador para el final del rango de códigos numéricos correspondientes a los eventos de error de TVSDK.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>15</td>
    <td>El tiempo de búsqueda proporcionado no es válido.</td>
  </tr>
  <tr>
    <td>AUDIO_TRACK_ERROR</td>
    <td>16</td>
    <td>Error relacionado con una pista de audio (audio alternativo)</td>
  </tr>
  <tr>
    <td>ACCESS_FROM_DIFFERENT_THREAD</td>
    <td>17</td>
    <td>La API de PSDK se llama desde un subproceso distinto al subproceso en el que se inicializó PSDK.</td>
  </tr>
  <tr>
    <td>ELEMENT_NOT_FOUND</td>
    <td>18</td>
    <td>No se encuentra el elemento.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>19</td>
    <td>Característica no implementada.</td>
  </tr>
  <tr>
    <td>PRE_ROLL_DISABLED</td>
    <td>20</td>
    <td>La preconfiguración se ha deshabilitado mediante AdvertisingMetadata.</td>
  </tr>
  <tr>
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>La reproducción de HLS no se ha activado en Flash Player. Consulte AuthorizedFeatures.enableMediaPlayerHLSPlayback().</td>
  </tr>
  <tr>
    <td>NETWORK_TIMEOUT</td>
    <td>58</td>
    <td>Se agotó el tiempo de espera de la red al recuperar un recurso o servidor de conexión.</td>
  </tr>
</table>

## Advertencias

La siguiente tabla proporciona información detallada sobre las notificaciones de tipo WARN.
La mayoría de las advertencias contienen metadatos relevantes; por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Nombre del error</b></th>
    <th><b>Código</b></th>
    <th><b>Descripción</b></th>
  </tr>
  <tr>
    <td>PLAYBACK_OPERATION_FAILED</td>
    <td>200</td>
    <td>Error durante la operación de reproducción. Error en una operación relacionada con la reproducción</td>
  </tr>
  <tr>  
    <td>NATIVE_WARNING</td>
    <td>201</td>
    <td>La biblioteca AVE de bajo nivel ha generado un error.</td>
  </tr>
  <tr>
    <td>AD_RESOLVER_FAILED</td>
    <td>202</td>
    <td>El complemento de publicidad no pudo resolver las publicidades.</td>
  </tr>
  <tr>
    <td>AD_MANIFEST_LOAD_FAILED</td>
    <td>203</td>
    <td>No se pudo cargar el manifiesto de publicidad.</td>
  </tr>
  <tr>
    <td>AD_RESOLUTION_IN_PROGRESS</td>
    <td>204</td>
    <td>La operación para resolver publicidades está en curso.</td>
  </tr>
  </table>

## Información

<table frame="all" colsep="1" rowsep="1">
  <tr> 
    <th><b>Nombre del error</b></th>
    <th><b>Código</b></th>
    <th><b>Descripción</b></th>
  </tr>
  <tr>
    <td>REVENUE_OPTIMIZATION_REPORTING</td>
    <td>300</td>
    <td>Notificaciones detalladas de TVSDK para informes y análisis posteriores.</td>
  </tr>
 </table>

## Códigos de error nativos

La interfaz del codificador de vídeo del AVE devuelve estas notificaciones de reproducción de vídeo en el objeto de metadatos NATIVE_ERROR.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Nombre del error</b></th>
    <th><b>Código</b></th>
    <th><b>Descripción</b></th>
  </tr>
  <tr>  
    <td>END_OF_PERIOD</td>
    <td>-1</td>
    <td>Fin del período.</td>
  </tr>
  <tr>
    <td>ÉXITO</td>
    <td>0</td>
    <td>Operación correcta.</td>
  </tr>
  <tr>
    <td>ASYNC_OPERATION_IN_PROGRESS</td>
    <td>1</td>
    <td>Operación asincrónica. Se ha realizado la solicitud de operación. La información de éxito y error estará disponible más adelante.</td>
  </tr>
  <tr>
    <td>EOF</td>
    <td>2</td>
    <td>La operación no es posible debido a la condición de fin de archivo (EOF).</td>
  </tr>
  <tr>
    <td>DECODER_FAILED</td>
    <td>3</td>
    <td>Error del decodificador en tiempo de ejecución.</td>
  </tr>
  <tr>
    <td>DEVICE_OPEN_ERROR</td>
    <td>4</td>
    <td>No se pudo abrir el descodificador de hardware.</td>
  </tr>
  <tr>
    <td>FILE_NOT_FOUND</td>
    <td>5</td>
    <td>No se encuentra el recurso.</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>6</td>
    <td>Error genérico.</td>
  </tr>
  <tr>
    <td>IRRECOVERABLE_ERROR</td>
    <td>7</td>
    <td>Condición de error de la que no se puede recuperar el motor de vídeo.</td>
  </tr>
  <tr>
    <td>LOST_CONNECTION_RECOVERABLE</td>
    <td>8</td>
    <td>Error de red al intentar recuperarse.</td>
  </tr>
  <tr> 
    <td>NO_FIXED_SIZE</td>
    <td>9</td>
    <td>No se puede determinar el tamaño del recurso.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>10</td>
    <td>Característica no implementada.</td>
  </tr>
  <tr>
    <td>OUT_OF_MEMORY</td>
    <td>11</td>
    <td>Memoria insuficiente.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR</td>
    <td>12</td>
    <td>Error al analizar el archivo multimedia.</td>
  </tr>
  <tr>  
    <td>SIZE_UNKNOWN</td>
    <td>13</td>
    <td>El recurso tiene un tamaño, pero se desconoce.</td>
  </tr>
  <tr>  
    <td>UNDER_FLOW</td>
    <td>14</td>
    <td>Condición de subdesbordamiento.</td>
  </tr>
  <tr> 
    <td>UNSUPPORTED_CONFIG</td>
    <td>15</td>
    <td>No se admite la configuración.</td>
  </tr>
  <tr>  
    <td>UNSUPPORTED_OPERATION</td>
    <td>16</td>
    <td>No se admite la operación.</td>
  </tr>
  <tr>
    <td>WAITING_FOR_INIT</td>
    <td>17</td>
    <td>Aún no se ha inicializado.</td>
  </tr>
  <tr>  
    <td>INVALID_PARAMETER</td>
    <td>18</td>
    <td>Parámetro no válido.</td>
  </tr>
  <tr>
    <td>INVALID_OPERATION</td>
    <td>19</td>
    <td>Operación no permitida.</td>
  </tr>
  <tr>
    <td>OP_ONLY_ALLOWED_IN_PAUSED_STATE</td>
    <td>20</td>
    <td>La operación solo está permitida mientras está en pausa.</td>
  </tr>
  <tr> 
    <td>OP_INVALID_WITH_AUDIO_ONLY_FILE</td>
    <td>21</td>
    <td>La operación no se puede utilizar en archivos de solo audio.</td>
  </tr>
  <tr>
    <td>PREVIOUS_STEP_SEEK_IN_PROGRESS</td>
    <td>22</td>
    <td>La operación de búsqueda anterior aún está en curso.</td>
  </tr>
  <tr> 
    <td>SOURCE_NOT_SPECIFIED</td>
    <td>23</td>
    <td>Recurso no especificado.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>24</td>
    <td>El valor especificado está fuera de rango.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>25</td>
    <td>Tiempo de búsqueda no válido.</td>
  </tr>
  <tr>
    <td>FILE_STRUCTURE_INVALID</td>
    <td>26</td>
    <td>El archivo especificado no se ajusta a la sintaxis esperada.</td>
  </tr>
  <tr>
    <td>COMPONENT_CREATION_FAILURE</td>
    <td>27</td>
    <td>No se pudo crear un componente esencial.</td>
  </tr>
  <tr>
    <td>DRM_INIT_ERROR</td>
    <td>28</td>
    <td>No se pudo crear el contexto de DRM.</td>
  </tr>
  <tr>
    <td>CONTAINER_NOT_SUPPORTED</td>
    <td>29</td>
    <td>No se admite el tipo de contenedor.</td>
  </tr>
  <tr>
    <td>SEEK_FAILED</td>
    <td>30</td>
    <td>La búsqueda falló.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>31</td>
    <td>Códec no admitido.</td>
  </tr>
  <tr>
    <td>NETWORK_UNAVAILABLE</td>
    <td>32</td>
    <td>La red no está disponible.</td>
  </tr>
  <tr>  
    <td>NETWORK_ERROR</td>
    <td>33</td>
    <td>Error al obtener datos de la red.</td>
  </tr>
  <tr>
    <td>DESBORDAMIENTO</td>
    <td>34</td>
    <td>Desbordamiento.</td>
  </tr>
  <tr>  
    <td>VIDEO_PROFILE_NOT_SUPPORTED</td>
    <td>35</td>
    <td>Perfil de vídeo no admitido.</td>
  </tr>
  <tr>
    <td>PERIOD_NOT_LOADED</td>
    <td>36</td>
    <td>Se intentó una operación en un período HOLD o un período que aún no se ha cargado.</td>
  </tr>
  <tr> 
    <td>INVALID_REPLACE_DURATION</td>
    <td>37</td>
    <td>La duración de reemplazo especificada no es válida o se extiende más allá del final del flujo.</td>
  </tr>
  <tr>
    <td>CALLED_FROM_WRONG_THREAD</td>
    <td>38</td>
    <td>No se puede llamar a la API desde el subproceso incorrecto. Principalmente, para elementos de API a los que solo se debe llamar desde el subproceso principal.</td>
  </tr>
  <tr>
    <td>FRAGMENT_READ_ERROR</td>
    <td>39</td>
    <td>Error de lectura del fragmento. No hay conmutación por error. El motor intentará leer el siguiente fragmento.</td>
  </tr>
  <tr>
    <td>ABORTADO</td>
    <td>40</td>
    <td>La operación se anuló mediante una llamada explícita a Anular o Destruir.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_HLS_VERSION</td>
    <td>41</td>
    <td>No se puede reproducir esta versión de medios HLS.</td>
  </tr>
  <tr>
    <td>CANNOT_FAIL_OVER</td>
    <td>42</td>
    <td>No se puede devolver el error.</td>
  </tr>
  <tr> 
    <td>HTTP_TIME_OUT</td>
    <td>43</td>
    <td>Se agotó el tiempo de espera de la descarga HTTP.</td>
  </tr>
  <tr>
    <td>NETWORK_DOWN</td>
    <td>44</td>
    <td>La conexión de red del usuario no funciona. La reproducción puede detenerse en cualquier momento y se reanudará cuando la conexión esté disponible.</td>
  </tr>
  <tr>
    <td>NO_USABLE_BITRATE_PROFILE</td>
    <td>45</td>
    <td>No se encontró ningún perfil de velocidad de bits utilizable en el flujo.</td>
  </tr>
  <tr>
    <td>BAD_MANIFEST_SIGNATURE</td>
    <td>46</td>
    <td>El manifiesto tiene una mala firma. Error en la prueba de firma de manifiesto.</td>
  </tr>
  <tr>
    <td>CANNOT_LOAD_PLAYLIST</td>
    <td>47</td>
    <td>No se puede cargar una lista de reproducción.</td>
  </tr>
  <tr>
    <td>REPLACEMENT_FAILED</td>
    <td>48</td>
    <td>El reemplazo especificado en una API de inserción no se pudo realizar correctamente. Esto significa que la inserción se realizó correctamente, pero la sustitución no. La sustitución podría fallar si el manifiesto que se va a reemplazar se ha eliminado de la línea de tiempo.</td>
  </tr>
  <tr>
    <td>SWITCH_TO_ASYMMETRIC_PROFILE</td>
    <td>49</td>
    <td>DRM está cambiando a un perfil asimétrico. Se espera que todos los perfiles estén alineados en la duración. De lo contrario, se emitirá esta advertencia y es posible que haya saltos en la reproducción.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_BACKWARD</td>
    <td>50</td>
    <td>Se espera que la ventana en directo solo avance. De lo contrario, se emitirá esta advertencia y la ventana no se leerá. Debido a esto, puede haber saltos (o detención/pausa prolongada) en la reproducción.</td>
  </tr>
  <tr>
    <td>CURRENT_PERIOD_EXPIRED</td>
    <td>51</td>
    <td>La ventana activa se ha movido más allá del período actual.</td>
  </tr>
  <tr>
    <td>CONTENT_LENGTH_MISMATCH</td>
    <td>52</td>
    <td>La longitud del contenido informada por el servidor HTTP no coincide con el tamaño real del medio.</td>
  </tr>
  <tr>
    <td>PERIOD_HOLD</td>
    <td>53</td>
    <td>El lector de medios no puede leer más porque ha alcanzado el tiempo establecido por la API setHoldAt.</td>
  </tr>
  <tr>  
    <td>LIVE_HOLD</td>
    <td>54</td>
    <td>El lector de medios no puede cargar segmentos porque ha llegado al final de la ventana activa. La carga de segmentos se reanudará cuando el servidor añada nuevos medios a la ventana activa. Este estado suele alcanzarse si:<ul><li>BufferTime es demasiado alto (igual o superior a la duración de la ventana activa).</li><li>Una combinación de una o más API de inserción/borrado reemplazó a más medios de los que agregaba.</li><li>El período siguiente es un período activo con un reemplazo de medios pendiente (debido a la llamada de la API InsertBy)</li></ul></td>
  </tr>
  <tr>
    <td>BAD_MEDIA_INTERLEAVING</td>
    <td>55</td>
    <td>La intercalación de audio y vídeo en los medios no se realiza correctamente. Se trata de un error de empaquetado. La advertencia se envía cuando la diferencia supera los dos segundos.</td>
  </tr>
  <tr>
    <td>DRM_NOT_AVAILABLE</td>
    <td>56</td>
    <td></td>
  </tr>
  <tr>  
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>La reproducción de HLS no se ha activado en Flash Player. Consulte AuthorizedFeatures.enableHLSPlayback.</td>
  </tr>
  <tr>
    <td>BAD_MEDIA_SAMPLE_FOUND</td>
    <td>58</td>
    <td>El decodificador recibió una muestra incorrecta que no se puede descodificar. Normalmente, no se trata de un error grave, pero indica que puede haber problemas en el audio o el vídeo. Demasiadas instancias de este error indican una codificación incorrecta o un archivo incorrecto.</td>
  </tr>
  <tr>
    <td>RANGE_SPANS_READ_HEAD</td>
    <td>59</td>
    <td>Una vez iniciada la reproducción, el rango Insertar/Reemplazar no debe contener el encabezado de lectura.</td>
  </tr>
  <tr> 
    <td>POSTROLL_WITH_LIVE_NOT_ALLOWED</td>
    <td>60</td>
    <td>Las inserciones posteriores al lanzamiento no están permitidas en un medio activo. Sin embargo, se permiten después de que el servidor marca el medio como completo.</td>
  </tr>
  <tr>
    <td>INTERNAL_ERROR</td>
    <td>61</td>
    <td>Un tema muy raro que nunca debería ocurrir.</td>
  </tr>
  <tr>  
    <td>SPS_PPS_FOUND_OUTSIDE_AVCC</td>
    <td>62</td>
    <td>El flujo no sigue la recomendación de empaquetado de colocar siempre H264 SPS/PPS en un AVCC. Es posible que se vean problemas de búsqueda/reproducción.</td>
  </tr>
  <tr>  
    <td>PARTIAL_REPLACEMENT</td>
    <td>63</td>
    <td>El reemplazo especificado en una API de inserción solo se realizó parcialmente. Esto sucede cuando replaceDuration se extiende sobre la duración de la línea de tiempo.</td>
  </tr>
  <tr>
    <td>RENDITION_M3U8_ERROR</td>
    <td>64</td>
    <td>Error al cargar la lista de reproducción de representación. Esto es solo para AVE, no para FlashPlayer.</td>
  </tr>
  <tr>
    <td>NULL_OPERATION</td>
    <td>65</td>
    <td>La operación no hace nada.</td>
  </tr>
  <tr>
    <td>SEGMENT_SKIPPED_ON_FAILURE</td>
    <td>66</td>
    <td>No se puede reproducir el segmento y se omite si se produce un error.</td>
  </tr>
  <tr>
    <td>INCOMPATIBLE_RENDER_MODE</td>
    <td>67</td>
    <td>Modo de procesamiento incompatible.</td>
  </tr>
  <tr>
    <td>PROTOCOL_NOT_SUPPORTED</td>
    <td>68</td>
    <td>No se admite el protocolo Web utilizado en la dirección URL.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR_INCOMPATIBLE_VERSION</td>
    <td>69</td>
    <td>Error al analizar el archivo multimedia.</td>
  </tr>
  <tr>  
    <td>MANIFEST_FILE_UNEXPECTEDLY_CHANGED</td>
    <td>70</td>
    <td>El archivo de manifiesto se cambió de forma inesperada.</td>
  </tr>
  <tr>
    <td>CANNOT_SPLIT_TIMELINE</td>
    <td>71</td>
    <td>No se puede realizar una operación de división en una línea de tiempo.</td>
  </tr>
  <tr>
    <td>CANNOT_ERASE_TIMELINE</td>
    <td>72</td>
    <td>No se puede realizar una operación de borrado en una línea de tiempo.</td>
  </tr>
  <tr>
    <td>DID_NOT_GET_NEXT_FRAGMENT</td>
    <td>73</td>
    <td>No se obtuvo el siguiente fragmento.</td>
  </tr>
  <tr>
    <td>NO_TIMELINE</td>
    <td>74</td>
    <td>No hay una línea de tiempo presente en una estructura de datos interna.</td>
  </tr>
  <tr>
    <td>LISTENER_NOT_FOUND</td>
    <td>75</td>
    <td>No se encontró ningún detector en una estructura de datos interna.</td>
  </tr>
  <tr>
    <td>AUDIO_START_ERROR</td>
    <td>76</td>
    <td>No se puede iniciar el audio.</td>
  </tr>
  <tr>
    <td>NO_AUDIO_SINK</td>
    <td>77</td>
    <td>No hay un receptor de audio presente en una estructura de datos interna.</td>
  </tr>
  <tr>  
    <td>FILE_OPEN_ERROR</td>
    <td>78</td>
    <td>No se puede abrir el archivo.</td>
  </tr>
  <tr>
    <td>FILE_WRITE_ERROR</td>
    <td>79</td>
    <td>No se puede escribir en un archivo.</td>
  </tr>
  <tr>
    <td>FILE_READ_ERROR</td>
    <td>80</td>
    <td>No se puede leer de un archivo.</td>
  </tr>
  <tr>
    <td>ID3PARSE_ERROR</td>
    <td>81</td>
    <td>Error al analizar los datos de ID3.</td>
  </tr>
  <tr>
    <td>SECURITY_ERROR</td>
    <td>82</td>
    <td>Error al cargar el contenido debido a restricciones de seguridad.</td>
  </tr>
  <tr>
    <td>TIMELINE_TOO_SHORT</td>
    <td>83</td>
    <td>La duración de la línea de tiempo es demasiado corta. Si se trata de un flujo en directo, puede ocurrir un almacenamiento en búfer frecuente.</td>
  </tr>
  <tr>
    <td>AUDIO_ONLY_STREAM_START</td>
    <td>84</td>
    <td>El flujo se ha cambiado a un flujo de solo audio.</td>
  </tr>
  <tr>  
    <td>AUDIO_ONLY_STREAM_END</td>
    <td>85</td>
    <td>El flujo se ha cambiado de solo audio a un flujo con vídeo.</td>
  </tr>
  <tr>
    <td>KEY_NOT_FOUND</td>
    <td>87</td>
    <td>No se encuentra la clave.</td>
  </tr>
  <tr>
    <td>INVALID_KEY</td>
    <td>88</td>
    <td>La clave no es válida.</td>
  </tr>
  <tr>
    <td>KEY_SERVER_NOT_FOUND</td>
    <td>89</td>
    <td>El servidor de claves no devuelve una clave.</td>
  </tr>
  <tr>
    <td>MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</td>
    <td>90</td>
    <td>No se puede gestionar la actualización de manifiesto principal.</td>
  </tr>
  <tr>
    <td>UNREPORTED_TIME_DISCONTINUITY_FOUND</td>
    <td>91</td>
    <td>Se encontró una discontinuidad de tiempo no informado (PTS).</td>
  </tr>
  <tr>
    <td>UNMATCHED_AV_DISCONTINUITY_FOUND</td>
    <td>92</td>
    <td>Se encontró una discontinuidad de audio y vídeo no coincidente.</td>
  </tr>
  <tr>
    <td>TRICKPLAY_ENDED_DUE_TO_ERROR</td>
    <td>93</td>
    <td>Se produjo un error al reproducir medios en el modo de reproducción mediante trucos. El modo de reproducción de trucos finaliza y el flujo se pone en pausa. Llame a Play() para reproducir el medio en modo normal.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_AHEAD</td>
    <td>95</td>
    <td>El jugador está fuera de la ventana activa y debe buscar hacia delante para ponerse al día.</td>
  </tr>
</table>
