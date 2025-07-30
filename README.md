# Proyecto-Alcoholimetro
Este sistema implementa una prueba de condición basada en biometría facial, diseñada para evaluar si una persona se encuentra en condiciones adecuadas para conducir o realizar una tarea crítica. Integra reconocimiento facial, calibración personalizada y evaluación en tiempo real de parámetros fisiológicos como el parpadeo y el cabeceo.

🔍 Funcionamiento general
Reconocimiento facial:

Se autentica al usuario mediante una base de datos de rostros conocidos usando la biblioteca face_recognition (integrada como SimpleFacerec).

Si el usuario no es reconocido, no se permite continuar.

Calibración personalizada:

Se ejecuta una fase de calibración de 30 segundos donde se capturan:

EAR promedio (Eye Aspect Ratio) como referencia.

Posición vertical de la nariz.

Ancho facial.

Estos datos se almacenan en un archivo .json para uso posterior.

Prueba de condición:

Se monitorea al usuario durante 30 segundos midiendo:

Parpadeos por minuto (PPM).

Cabeceos por minuto (CPM).

Se calculan ambos valores y se comparan contra los umbrales derivados de la calibración.

Criterios de alerta:

Si el PPM es significativamente mayor al valor base (por ejemplo, >150% del EAR de referencia).

O si el CPM supera un límite razonable (por ejemplo, más de 5 cabeceos por minuto).

Se emite una advertencia en consola y en pantalla, indicando que la persona podría estar fatigada o afectada.

📂 Estructura de datos de calibración
json
Copy
Edit
{
  "baseline_ear": 5.6,
  "baseline_nose_y": 123,
  "face_width_ref": 154,
  "timestamp": "2025-05-23 10:00:00"
}
🧠 Lógica del sistema (resumen técnico)
El EAR se calcula con los landmarks de los ojos (puntos 36-47 del modelo shape_predictor_68_face_landmarks.dat).

El cabeceo se determina por la variación vertical del punto 30 (punta de la nariz), ajustada por el ancho facial.

Se emplea un trimmean para eliminar valores atípicos durante la calibración.

La cámara es accedida con OpenCV (cv2.VideoCapture(0)).

La prueba se detiene si el usuario presiona ESC.

⚙️ Dependencias principales
OpenCV (cv2)

dlib y shape_predictor_68_face_landmarks.dat

face_recognition

numpy, scipy, json, time, os, sys

