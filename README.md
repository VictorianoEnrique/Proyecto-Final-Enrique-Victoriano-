# Proyecto-Final-Enrique-Victoriano-Evaluación de la fatiga neuromuscular durante el ejercicio (ECG-EMG).

Esta herramienta es una interfaz gráfica (GUI) diseñada en MATLAB App Designer para adquirir y procesar señales biomédicas (ECG y EMG) en tiempo real mediante tareas simultáneas. El sistema procesa los datos en bloques usando ventanas deslizantes, lo que permite detectar de forma automática cuándo aparece la fatiga neuromuscular durante ejercicios isométricos sostenidos.

Requisitos del Sistema

Para correr la aplicación sin problemas, necesitas el siguiente entorno y librerías:

Software Base: MATLAB (Versión R2020a o superior recomendada).

Toolboxes Oficiales de MATLAB (Obligatorios):

Signal Processing Toolbox: Necesario para el cálculo de la Transformada de Fourier de Tiempo Corto (STFT), densidad espectral de potencia (fft) y detección de picos QRS (findpeaks).

MATLAB App Designer: Entorno nativo donde está construida la interfaz gráfica.

Formato de Datos: Archivos de texto o datos (.txt o .dat) exportados de sistemas clínicos como BIOPAC o hardware embebido.
Deben venir en columnas separadas por tabuladores (Columna 1: ECG, Columna 2: EMG).


Guía de Instalación y Ejecución Rápida

Clonar o descargar el repositorio:
git clone [https://github.com/MrSkipper-byte/Evaluaci-n-de-la-fatiga-neuromuscular-durante-el-ejercicio-EMG-ECG-.git)

Abre MATLAB y muévete desde el Current Folder hasta la carpeta /Software del proyecto.


Lanza la app

Haz doble clic en el archivo AppBiopack.mlapp (o el script .m generado por App Designer).

Alternativamente, escribe en la ventana de comandos de MATLAB:
AppBiopack

La interfaz gráfica se abrira automáticamente.


Como usar GUI

Paso 1: Importación de Datos Biomédicos

Ve a la esquina superior izquierda y haz click en "Importar".
Busca y selecciona el archivo con el registro del sujeto de prueba.
La app cargará las señales y armará los vectores de tiempo de forma automática basándose en una frecuencia de muestreo fija de 
2000Hz (fs = 2000).


Paso 2: Calibración Automática (Primeros 8 Segundos)

Al cargar el archivo, un timer interno arranca la simulación y empieza a refrescar las gráficas en tiempo real.
Durante los primeros 8 segundos, el sistema entra en una fase de Calibración (verás los textos BPM: Calibrando... y Estado Músculo: Calibrando...).
En este lapso, el algoritmo promedia las señales iniciales para calcular la Frecuencia Mediana (MDF) Base (músculo en estado normal) y los BPM Base (ritmo cardíaco en reposo).

Paso 3: Monitoreo y Criterio de Fatiga

Gráficas en vivo: La pantalla muestra tres señales en constante actualización:
Ventana móvil de 2 segundos del ECG.
Ventana móvil de 2 segundos del EMG (ya filtrado y centrado).
La evolución segundo a segundo de la Frecuencia Mediana (MDF) calculada con STFT.
¿Cómo detecta la fatiga? Pasados los 8 segundos de calibración, el código cruza dos variables en tiempo real:
Que la MDF del EMG caiga por debajo del 75% de su valor base (indicador directo de fatiga muscular).
Que la frecuencia cardíaca (BPM) se mantenga por encima de las pulsaciones base.


Paso 4: Activación de Alertas

Si el sujeto cumple ambas condiciones al mismo tiempo, el indicador visual cambia de verde (Estado Músculo: Normal) a rojo brillante con el mensaje "FATIGA DETECTADA".
Además, la app activará un beep intermitente que no dejará de sonar mientras el músculo siga fatigado.
Capturas de Pantalla de la GUI en Funcionamiento

<img width="1600" height="852" alt="image" src="https://github.com/user-attachments/assets/c5afe761-1a48-4491-87ee-7fa5dd0aeee2" />

<img width="1600" height="852" alt="image" src="https://github.com/user-attachments/assets/4fc68cd3-dae0-4669-bffa-faa93d1e414f" />


