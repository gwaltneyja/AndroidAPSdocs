# Configuraciones

Dependiendo de sus ajustes, puede abrir el administrador de configuraciones a través de una pestaña en la parte superior de la pantalla o a través del menú de la hamburguesa.

![Abrir configuraciones](../images/ConfBuild_Open.png)

Configuraciones (Conf.) es la pestaña en la donde se activan y desactivan las características modulares. Las opciones en el lado izquierdo (A) le permiten seleccionar cuál utilizar, las opciones del lado derecho (C) le permiten ver estas como pestañas. (E) en AndroidAPS. En caso de que el recuadro correcto no esté activado, puede llegar a la función utilizando el menú de hamburguesa (D) en la parte superior izquierda de la pantalla.

Cuando hay opciones adicionales disponibles en el módulo, puede hacer clic en la rueda dentada (B), que te llevará a la configuración específica dentro de las preferencias.

**Primera configuración:** En AAPS 2.0 un asistente de instalación le guía a través del proceso de configuración de AndroidAPS. Presione los 3 puntos en la parte superior derecha de la pantalla (F) y seleccione 'Asistente de configuración' para usarlo.

![Caja de configuraciones y engranaje](../images/ConfBuild_ConfigBuilder.png)

## Pestañas o menú de hamburguesa

Con la casilla de verificación, bajo el símbolo de ojo, puede decidir cómo abrir la sección correspondiente del programa.

![Pestañas o menú de hamburguesa](../images/ConfBuild_TabOrHH.png)

## Perfil

Seleccione el perfil basal que desea utilizar. Consulte la página [Perfiles](../Usage/Profiles.md) para obtener más información de configuración.

### Perfil local (recomendado)

El "perfil local" utiliza el perfil basal manualmente ingresado en el teléfono. Tan pronto como se selecciona, aparece una nueva pestaña en AAPS, donde puede cambiar los datos de perfil leídos de la bomba si es necesario. Con la tecla siguiente, el perfil se escriben en la bomba en el perfil 1. Este perfil se recomienda ya que no depende de la conectividad a Internet.

Ventajas:

* no hay ninguna conexión a Internet necesaria para cambiar los valores de perfil
* los cambios de perfil se pueden hacer directamente en el teléfono

Desventajas:

* sólo un perfil

### Perfil NS

El perfil de NS utiliza los perfiles que guardados en el sitio de Nightscout (https: //[yournightscoutsiteaddress]/profile). Puede usar el [Selector de Perfil](../Usage/Profiles.md) para cambiar cuál de los perfiles está activo, y se escribe ese perfil en la bomba en caso de fallo AndroidAPS. Esto le permite crear fácilmente múltiples perfiles en Nightscout (p.ej.. trabajo, casa, deportes, vacaciones, etc.). Poco después de hacer clic en "Guardar" serán transferidos a AAPS si su smartphone está en línea. Incluso sin conexión a Internet o sin conexión a Nightscout, los perfiles de Nightscout están disponibles en AAPS una vez que se han sincronizado.

Realice un **cambio de perfil** para activar un perfil de Nightscout. Mantén pulsado el perfil actual en la pantalla de inicio AAPS en la parte superior (campo gris entre el campo azul claro "Lazo Abrierto/Cerrado" y el campo azul oscuro Objetivo) > Cambio de perfil > Seleccionar perfil > Aceptar. AAPS también escribe el perfil seleccionado en la bomba después de que el cambio de perfil, de modo que esté disponible sin AAPS en caso de emergencia y continúa su ejecución.

Ventajas:

* perfiles múltiples
* fácil de editar por PC o tablet

Desventajas:

* no hay cambios locales en los ajustes de perfil
* el perfil no puede ser cambiado directamente en el teléfono

### Perfil simple

Perfil simple con sólo un bloque de tiempo para DIA, IC, ISF, tasa basal y rango de objetivo (es decir, sin cambios en la tasa basal durante el día). Es más probable que se utilice para fines de prueba a menos que tenga los mismos factores durante las 24 horas. Una vez seleccionado "Perfil simple", aparecerá una nueva pestaña en AAPS donde puede introducir los datos del perfil.

## Insulina

Seleccione el tipo de curva de insulina que está usando. Las opciones 'Rapid-Acting Oref', Ultra-Rapid Oref' y 'Free-Peak Oref' tienen una forma exponencial. Más información disponible en [OpenAPS docs](http://openaps.readthedocs.io/en/latest/docs/While%20You%20Wait%20For%20Gear/understanding-insulin-on-board-calculations.html#understanding-the-new-iob-curves-based-on-exponential-activity-curves), las curvas varían según el DIA y el tiempo de pico de acción.

La DIA no es la misma para cada persona. Es por eso que tienes que probarlo por ti mismo. Pero siempre debe ser de al menos 5 horas. Puede leer más sobre esto en la sección Perfil de Insulina de [aqui](../Getting-Started/Screenshots#insulin-profile).

Para Rapid-Acting y Ultra-Rapid, el DIA es la única variable que se puede ajustar por ti mismo, el tiempo de pico de acción es fijo. Free-Peak te permite ajustar tanto el DIA como el tiempo hasta el pico, y sólo debe ser utilizado por los usuarios avanzados que conocen los efectos de estos ajustes.

El [gráfico de la curva de insulina](../Getting-Started/Screenshots#insulin-profile) le ayuda a comprender las diferentes curvas. Puede verlo habilitando la casilla de verificación para mostrarla como una pestaña, de lo contrario estará en el menú hamburgesa.

### Rapid-Acting Oref

* recomendado para Humalog, Novolog y Novorapid
* DIA = al menos 5.0h
* Máximo pico = 75 minutos después de la inyección (fijo, no ajustable)

### Ultra-Rapid Oref

* recomendado para FIASP
* DIA = al menos 5.0h
* Máximo pico = 55 minutos después de la inyección (fijo, no ajustable)

Para mucha gente no hay prácticamente ningún efecto visible de FIASP después de 3-4 horas es más, incluso si las unidades 0.0xx están disponibles como regla entonces. Esta cantidad residual puede percibirse durante los deportes, por ejemplo. Por lo tanto, AndroidAPS utiliza el mínimo de 5h como DIA.

![Configuración Ultra-Rapid Oref](../images/ConfBuild_UltraRapidOref.png)

### Free-Peak Oref

Con el perfil "Free Peak 0ref" usted puede ingresar individualmente el tiempo del pico. El DIA se establece automáticamente en 5 horas si no se especifica un valor superior en el perfil.

Este perfil de efecto se recomienda si se utiliza una insulina no respaldada o una mezcla de insulinas diferentes.

## Fuentes de BG (datos de glucemia)

Seleccione la fuente de glucosa en sangre que está utilizando: consulte la página [BG Fuentes ](BG-Source.rst) para obtener más información de configuración.

* [xDrip+](https://xdrip-plus-updates.appspot.com/stable/xdrip-plus-latest.apk)
* NSClient BG
* [MM640g](https://github.com/pazaan/600SeriesAndroidUploader/releases)
* [Glimp](https://play.google.com/store/apps/details?id=it.ct.glicemia&hl=de)
* [Dexcom App (parche) ](https://github.com/dexcomapp/dexcomapp/) -Seleccione 'Enviar datos de BG a xDrip +' si desea utilizar las alarmas xDrip +.
    
    ![Configurar origen de BG](../images/ConfBuild_BGSource.png)

* [Poctech](http://www.poctechcorp.com/en/contents/268/5682.html)

## Bomba

Seleccione la bomba que está utilizando.

* [Dana R](DanaR-Insulin-Pump.md)
* Dana R Coreano (para la bomba doméstica DanaR)
* Dana Rv2 (bomba DanaR con actualización de firmware)
* [Dana RS](DanaRS-Insulin-Pump.md)
* [Accu Chek Combo Pump ](Accu-Chek-Combo-Pump.md) (requiere la instalación de ruffy)
* MDI (recibir sugerencias de AAPS para su terapia de inyecciones múltiples diarias)
* Bomba virtual (bucle abierto para la bomba que no tiene ningún controlador todavía-sólo sugerencias de AAPS)

Utilice **Valores avanzados ** para activar el proceso de vigilancia de BT si es necesario. Desactiva bluetooth por un segundo si no es posible ninguna conexión a la bomba. Esto puede ayudar en algunos teléfonos donde la pila (Stack) Bluetooth se congela (freezes).

## Detección de sensibilidad

Seleccione el tipo de detección de sensibilidad. Esto analizará los datos históricos sobre la marcha y realizará ajustes si reconoce que está reaccionando con más sensibilidad (o a la inversa, más resistente) a la insulina de lo habitual. Los detalles sobre el algoritmo de Sensibilidad Oref0 se pueden leer en el [OpenAPS docs](http://openaps.readthedocs.io/en/latest/docs/walkthrough/phase-4/advanced-features.html#auto-sensitivity-mode).

Usted puede ver su sensibilidad en la pantalla de inicio seleccionando SEN y viendo la línea blanca. Tenga en cuenta que debe estar en [Objetivo 8 ](../Usage/Objectives#objective-8-adjust-basals-and-ratios-if-needed-and-then-enable-autosens) con el fin de utilizar Detección de sensibilidad/autosens.

### Ajustes absorción

Si utiliza Oref1 con SMB, debe cambiar **min_5m_carbimpact ** a 8. El valor sólo se utiliza durante las diferencias en las lecturas de MCG o cuando la actividad física "utiliza" todo el aumento de la glucosa en la sangre, lo que de otra manera causaría que la AAPS descienda a COB. A veces, cuando la absorción de carbohidratos no puede ser dinámicamente trabajada, en base a sus reacciones de sangre, inserta una baja por defecto en sus carbohidratos. Básicamente, es un seguro contra fallos.

## APS

Seleccione el algoritmo APS deseado para realizar los ajustes de la terapia. Puede ver los detalles activos del algoritmo elegido en la pestaña OpenAPS(OAPS).

* OpenAPS MA (asistencia para comidas, estado del algoritmo en 2016)
* OpenAPS AMA (asistencia de comida avanzada, estado del algoritmo en 2016)   
    Más detalles acerca de OpenAPS AMA se pueden encontrar en [OpenAPS docs ](http://openaps.readthedocs.io/en/latest/docs/Customize-Iterate/autosens.html#advanced-meal-assist-or-ama). En términos simples, los beneficios son después de que se pone un bolo de comida, que el sistema puede ser más rápido si especifica los carbohidratos de forma fiable.   
    Note que necesita estar en [Objetivo 9 ](../Usage/Objectives#objective-9-enabling-additional-oref0-features-for-daytime-use-such-as-advanced-meal-assist-ama) para poder utilizar OpenAPS AMA.
* [OpenAPS SMB](../Usage/Open-APS-features.md) (super micro bolo, el más reciente algoritmo para usuarios avanzados)  
    Nota: debe estar en [Objetivo 10](../Usage/Objectives#objective-10-enabling-additional-oref1-features-for-daytime-use-such-as-super-micro-bolus-smb) para utilizar OpenAPS SMB y min_5m_carbimpact debe estar ajustado a las 8 en el Config builder > Sensibilidad de detección > Valor de sensibilidad Oref1.

## Loop

Defina si quieres permitir controles automáticos AAPS o no.

### Lazo abierto

AAPS evalúa continuamente todos los datos disponibles (IOB, COB, BG...) y hace sugerencias de tratamiento sobre cómo ajustar su terapia si es necesario. Las sugerencias no se ejecutarán automáticamente (como en el lazo cerrado) deben introducirse manualmente en la bomba o usando un botón en caso de que esté usando una bomba compatible (Dana R/RS o Accu Chek Combo). Esta opción es para conocer cómo funciona AndroidAPS o si está usando una bomba no soportada.

### Lazo cerrado

AAPS evalúa continuamente todos los datos disponibles (IOB, COB, BG...) y ajusta automáticamente el tratamiento si es necesario (es decir, sin intervención adicional) para alcanzar el rango o valor de destino establecido (entrega de bolo, basal temporal, parada de infusión de insulina para evitar la hipoglucemia, etc.). El Loop Cerrado funciona dentro de numerosos límites de seguridad, que se pueden establecer individualmente. El Lazo Cerrado sólo es posible si está en [Objetivo 6 ](../Usage/Objectives#objective-6-starting-to-close-the-loop-with-low-glucose-suspend) o superior y utiliza una bomba soportada.

## Objetivos (programa de aprendizaje)

AndroidAPS tiene una serie de objetivos que tiene que cumplir paso a paso. Esto debería guiarle de forma segura hacia la configuración de un sistema de lazo cerrado. Esto garantiza que usted tiene configurado todo correctamente y que entienda lo que el sistema hace exactamente. Esta es la única forma en la que puedes confiar en el sistema.

Deberías [exportar tus ajustes](../Usage/ExportImportSettings.rst) (incluyendo el progreso de los objetivos) regularmente. En caso de que tenga que reemplazar su smartphone más tarde (compra de uno nuevo, daños de pantalla, etc.), simplemente puede importar estos ajustes.

Consulte la página [Objetivos](../Usage/Objectives.rst) para obtener más información de configuración.

## Tratamientos

Si ve la pestaña Tratamientos (Trat), usted puede ver los tratamientos que se han subido a nightscout. Si desea editar o eliminar una entrada (por ejemplo, si ha comido menos carbohidratos de lo que esperaba), seleccione 'Eliminar' y especifique el nuevo valor (cambie el tiempo si es necesario) a través de la pestaña Careportal (CP).

## General

### Inicio

Muestra el estado actual de su lazo y los botones para las acciones más comunes (ver [sección de La Pantalla de inicio](../Getting-Started/Screenshots.md) para obtener más detalles). Se puede acceder a los valores haciendo clic en el icono del engranaje.

#### Mantener pantalla activa

La opción 'Mantener pantalla encendida' obligará a Android a mantener la pantalla en todo momento. Esto es útil para presentaciones, etc. Pero que consume una gran cantidad de energía de la batería. Por lo tanto, se recomienda conectar el smartphone con un cable a un cargador.

#### Botones

Definir los Botones que se muestran en la pantalla de inicio.

* Tratamientos
* Calculadora
* Insulina
* Carbohidratos [g]
* MCG (abre xDrip +)
* Calibración

Además, puede establecer accesos directos para los incrementos de insulina y carb y decidir si el campo de notas debe mostrarse en los diálogos de tratamiento.

#### Asistente configuración

Crear un botón para una determinada comida estándar (carbohidratos y método de cálculo para el bolo) que se mostrará en la pantalla de inicio. Usar para comidas que se consumen con frecuencia. Si se especifican diferentes horas para las diferentes comidas, siempre tendrá el botón de comida adecuado en la pantalla de inicio, dependiendo de la hora del día.

Nota: el botón, no será visible si se encuentra fuera del intervalo de tiempo especificado, o si usted tiene suficiente IOB para cubrir los hidratos de carbono definidos en el botón Asistente rápido (QuickWizard).

![Configuración del asistente rápido](../images/ConfBuild_QuickWizard.png)

#### Ajustes avanzados

Habilite la funcionalidad de super bolo en el asistente. Utilícelo con precaución y no lo habilite hasta que aprenda lo que realmente hace. Básicamente, el basal para las próximas dos horas se añade al bolo y se activa un tiempo cero de dos horas. **Las funciones de lazo AAPS se inhabilitarán, por lo que se utilizará con precaución! Si utiliza las funciones de SMB, AAPS se inhabilitará de acuerdo con los valores en ["Máx minutos de basal para limitar SMB a" ](../Usage/Open-APS-features#max-minutes-of-basal-to-limit-smb-to), si no utiliza funciones de bucle de SMB se inhabilitarán durante dos horas. ** Detalles de super bolo pueden encontrarse [aquí ](https://www.diabetesnet.com/diabetes-technology/blue-skying/super-bolus).

### Acciones

Algunos botones para acceder rápidamente a funciones comunes:

* Conmutador de perfiles (consulte el apartado [Página de perfiles](../Usage/Profiles.md) para obtener más información de configuración)
* Objetivos temporales
* Establecer / cancelar temporal. dosis basal
* Bolo extendido (sólo la bomba DanaR/RS o Combo)
* Cebar / llenar (solo DanaR/RS o bomba de Combo)
* Navegador de Historial
* TDD (dosis diaria total = bolo + basal por día)

Algunos médicos usan -especialmente para los recién iniciados en las bombas- una relación basal-bolo de 50:50. Por lo tanto, la proporción se calcula como TDD / 2 * TBB (Total base basal = suma de la tasa basal en 24 horas). Otros prefieren un rango de 32% a 37% de TDD para TBB. Al igual que la mayoría de estas reglas empíricas, su validez real es limitada. Nota: ¡Tu diabetes puede variar!

![Pestaña de acciones](../images/ConfBuild_ConfBuild_Actions.png)

### Careportal

Le permite registrar cualquier entrada de tratamiento específico y ver el sensor actual, la insulina, la vida de la cánula y la batería de la bomba en la pestaña Careportal (CP).

Nota: **No se dará insulina** si se ingresa a través de careportal (por ejemplo, bolo de comida, corregir bolo...)

Los carbohidratos que se introducen en el portal (por ejemplo los de corrección) se utilizarán para el cálculo de la COB.

![Pestaña de tratamientos (Careportal)](../images/ConfBuild_CarePortal.png)

### Comunicaciones SMS

Permite a los cuidadores remotos controlar algunas características de AndroidAPS a través de SMS, ver [mandos SMS ](../Children/SMS-Commands.rst) para obtener más información de configuración.

### Comida

Muestra los valores de alimentos definidos en la base de datos de alimentos de Nightscout, consulte el apartado [Información de Nightscout](https://github.com/nightscout/cgm-remote-monitor#food-custom-foods) para obtener más información de configuración.

Nota: Las entradas no se pueden utilizar en la calculadora AndroidAPS. (Ver solamente)

### Reloj

Supervise y controle AAPS con su reloj Android Wear (vea [pagina de pantallas de reloj](../Configuration/Watchfaces.md)). Utilice la configuración (engranaje) para definir las variables que deben tenerse en cuenta a la hora de calcular el bolo dado a través de su reloj (por ejemplo, la tendencia de 15min, COB...).

Si desea bolo etc. desde el reloj entonces dentro de "Configuración de Reloj" que necesitas para activar "Controles desde el Reloj".

![Ajustes reloj](../images/ConfBuild_Wear.png)

A través de la pestaña Reloj o el menú de hamburguesas (la parte superior izquierda de la pantalla, si no se visualiza el tabulador) puede

* Reenviar todos los datos. Puede ser útil si el reloj no está conectado durante algún tiempo y desea enviar la información al reloj.
* Abre los ajustes en tu reloj directamente desde tu teléfono.

### Linea de estado xDrip (reloj)

Visualizar información del lazo en el reloj de xDrip + (si no está utilizando AAPS/[AAPSv2 watchface ](../Configuration/Watchfaces.md)

### Avisos permanentes

Visualiza un resumen del BG actual, delta, TBR% activo, basal activo u/h y perfil, IOB y se divide en IOB en bolo y basal IOB en la pantalla desplegable de los teléfonos y en la pantalla de bloqueo del teléfono.

![Widget de AAPS](../images/ConfBuild_Widget.png)

### NS Client

Configuración de la sincronización de datos de su AndroidAPS con Nightscout.

Si **Comenzar registro de app hacia NS** se activa cada dato de AndroidAPS será visible en Nightscout. Puede ser útil para detectar problemas con la aplicación (por ejemplo, la optimización de la batería no inhabilitada para AAPS), pero puede llenar el gráfico Nightscout con datos.

#### Opciones de alarma

Activar/desactivar alarmas AndroidAPS

![Opciones de alarma](../images/ConfBuild_NSClient_Alarms.png)

#### Ajustes conexión

Lazo sin conexión, desactivar roaming...

Si desea utilizar sólo una red WiFi específica, puede especificar su **SSID de WiFi **. Varios SSID se pueden separar mediante punto y coma. Para suprimir todos los SSID, introduzca un espacio en blanco en el campo.

![Configuración conexión de Nightscout](../images/ConfBuild_ConnectionSettings.png)

#### Ajustes avanzados

* Rellenar BGs perdidos desde NS
* Crear un anuncio a partir de los errores Crear anuncio de Nightscout para los diálogos de errores y alertas locales (también disponible en careportal en la sección de tratamientos)
* Permitir emisión de mensajes a otras aplicaciones como xDrip+
* Sólo carga de NS (sincronización inhabilitada)
* Datos no enviados a NS
* Utilice siempre los valores absolutos basales-> Debe activarse si desea utilizar [Autoajuste ](https://openaps.readthedocs.io/en/latest/docs/Customize-Iterate/autotune.html) correctamente.

![Ajustes avanzados de Nightscout](../images/ConfBuild_NSClient_Advanced.png)

### Mantenimiento

Correo electrónico y logs a enviar. Normalmente no es necesario ningún cambio.

### Configuraciones

Utilice la pestaña para configuraciones en lugar del menú hamburgesa.