**ÍNDICE**:
- 01_EDA_final.ipynb: Análisis de datos y tratamiento
- 02_modelo_lstm_final.ipynb: Entrenamiento y estudio del modelo LSTM
- 03_modelo_cnn_lstm_atencion_final.ipynb: Entrenamiento y análisis del modelo CNN-LSTM con capa de atención
- 04_modelo_transformer_final: Entrenamiento y análisis del modelo Tranformer encoder y comparativa de resultados con los demás modelos

🎯 **EL OBJETIVO**:
**Estimar la Vida Útil Restante (RUL)** de motores de turbofán a partir de series temporales de sensores, y determinar qué arquitectura equilibra mejor precisión, coste computacional e interpretabilidad.
Intervenir tarde es un fallo en operación. Intervenir pronto es tirar vida útil que aún quedaba.

🔧 **EL MÉTODO**:
Dataset **NASA C-MAPSS** y sus cuatro subconjuntos (FD001–FD004).
Pipeline reproducible: objetivo de degradación lineal a trozos, clustering no supervisado de los regímenes operativos, normalización dentro de cada régimen y ventanas deslizantes sin fuga de información.
Tres arquitecturas: LSTM apilada, CNN-LSTM con atención y codificador Transformer. Evaluadas con RMSE, MAE y la puntuación de NASA, que penaliza más sobreestimar la vida restante: el error peligroso.

📊 **LOS RESULTADOS**:
RMSE sobre FD001, media de tres semillas:
→ **LSTM**: 13,86 ± 0,19
→ **CNN-LSTM + atención**: 14,04 ± 0,24
→ **Transformer**: 14,15 ± 0,24
Una banda de 0,29 ciclos, menor que la incertidumbre de cualquier par de ellas. No hay diferencia. Y la LSTM, la más sencilla, gana en tres de los cuatro subconjuntos.
El orden sí cambia según la métrica: con RMSE equivalente, el Transformer obtiene la mejor puntuación de NASA. Y la atención, que concentra la lectura en el instante previo a la predicción, aporta interpretabilidad pero no precisión.
El hallazgo no es un error concreto: es que las diferencias entre las tres arquitecturas no superan el ruido experimental.

🧠 **LO QUE ME LLEVO**
→ EDA de series multivariantes: distribución de la vida útil, descarte de sensores sin varianza informativa, patrones de degradación.
→ Preprocesado de series: construcción de la variable objetivo, clustering de regímenes operativos, normalización por régimen, ventanas deslizantes sin fuga entre particiones.
→ Arquitecturas secuenciales en TensorFlow/Keras: LSTM apiladas, convoluciones 1D, atención aditiva y autoatención multi-cabeza con codificación posicional.
→ Diagnóstico de entrenamiento: curvas de aprendizaje, early stopping, saturación de ReLU y escalado de la variable objetivo.
→ Diseño experimental: métricas asimétricas de dominio, diseño factorial, estabilidad frente a la semilla y análisis de pesos de atención.

Calificación: 9,7.
