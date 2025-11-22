# 📘 README – Simulación PID de Pava Eléctrica Inteligente

## 🧩 1. Introducción

Este proyecto implementa una **simulación interactiva y animada** del control de temperatura de una pava eléctrica mediante un **controlador PID**.  
El objetivo es visualizar en **tiempo real** cómo el sistema reacciona frente a:

- Diferentes condiciones iniciales  
- Variaciones en los parámetros del controlador  
- Perturbaciones externas  
- Cambios en la dinámica de la planta  

La simulación muestra todas las señales fundamentales del lazo:

- **θ₀(t):** referencia (setpoint)  
- **θ(t):** salida del sistema (temperatura del agua)  
- **f(t):** realimentación  
- **e(t):** error  
- **u(t):** acción del controlador  
- **p(t):** perturbación aplicada  

Permite estudiar el **transitorio, el estacionario, la estabilidad y el rechazo de perturbaciones**, todo de manera visual e intuitiva.

---

## 🚀 2. Cómo ejecutar la simulación

1. Descargar la carpeta del proyecto.  
2. Abrir **`index.html`** con un navegador moderno (Chrome, Edge, Firefox).  

No requiere instalación, servidor ni conexión a internet.

---

## 🎛️ 3. Panel de controles

### 🔵 3.1 Señales principales

- **θ₀ – Temperatura nominal [°C]**  
  Es la temperatura objetivo que el controlador intenta mantener.

- **θ(0) – Temperatura inicial del agua [°C]**  
  Condición inicial de la planta. Puede iniciarse con agua fría o ya caliente.

---

### 🟢 3.2 Control PID
| Parámetro |                       Efecto                         |
|-----------|------------------------------------------------------|
| **Kp**    | Acelera la respuesta; demasiado alto → oscilaciones. |
| **Ki**    | Elimina error permanente; excesivo → inestabilidad.  |
| **Kd**    | Amortigua; demasiado → ruido.                        |

Los tres sliders pueden modificarse mientras la simulación está corriendo para observar sus efectos en tiempo real.

---

### 🟠 3.3 Perturbación p(t)

- **Amplitud:** magnitud de la perturbación (°C).  
- **Inicio:** segundo a partir del cual se aplica.  
- **Duración Δt:** cuánto tiempo actúa.

La perturbación modela, por ejemplo, una pérdida de calor repentina o un cambio brusco en el entorno.

---

### 🟣 3.4 Dinámica de la planta

- **τ – Constante de tiempo [s]**  
  - τ grande → pava lenta (respuesta más suave).  
  - τ chica → pava rápida (respuesta más agresiva).

---

## 🕹️ 4. Botones

- **Simular (animado):** inicia la simulación continua.  
- **Detener:** pausa la simulación en el estado actual.  
- **Valores razonables:** restaura un conjunto de parámetros estables por defecto.

Los sliders pueden moverse mientras la simulación está en marcha.

---

## 📈 5. Gráficos mostrados

### 5.1 Gráfico 1 – Señales externas

- **θ₀(t):** referencia (línea punteada).  
- **θ(t):** temperatura real del agua.  
- **p(t):** perturbación aplicada.

Se utiliza una ventana deslizante de ~20 segundos, tipo osciloscopio, para visualizar el comportamiento reciente del sistema.

---

### 5.2 Gráfico 2 – Señales internas

- **e(t):** error = θ₀ – θ(t).  
- **f(t):** realimentación = θ(t).  
- **u(t):** salida del controlador PID.

Este gráfico permite ver cómo actúa el controlador para corregir el error y estabilizar la temperatura.

---

## 🧮 6. Modelo matemático

### 6.1 Planta de primer orden

Se modela la pava eléctrica como un sistema de primer orden:

\[
\frac{d\theta}{dt} = -\frac{1}{\tau}(\theta - u(t)) + p(t)
\]

donde:

- **θ(t):** temperatura del agua.  
- **u(t):** señal de control (salida del PID).  
- **p(t):** perturbación.  
- **τ:** constante de tiempo de la planta.

---

### 6.2 Controlador PID (forma discreta)

La señal de error es:

\[
e(t) = \theta_0 - \theta(t)
\]

El control PID discreto implementado es:

\[
u(t) = K_p e(t) + K_i \int e(t) dt + K_d \frac{de}{dt}
\]

con integración acumulada y derivada aproximada por diferencias finitas.

---

### 6.3 Perturbación p(t)

Se implementa como un **pulso rectangular**:

- Amplitud definida por el slider.  
- Presente sólo entre \( t \in [t_{inicio}, t_{inicio} + \Delta t] \).  

---

## 🔍 7. Experimentos sugeridos

### ✔ Rechazo de perturbaciones
- θ₀ = 90°C  
- θ(0) = 90°C  
- Amplitud de perturbación: +10°C  
- Inicio: 10 s, duración: 4 s  

Se observa cómo el sistema vuelve al valor nominal luego de la perturbación.

---

### ✔ Análisis del transitorio

- θ(0) = 25°C  
- θ₀ = 85°C  

Permite ver la curva de calentamiento, el sobrepaso (si existe) y el tiempo de establecimiento.

---

### ✔ Inestabilidad (mala sintonización)

Probar, por ejemplo:

- **Kp > 7**  
- **Ki > 1**  
- **Kd ≈ 0**

Pueden observarse oscilaciones grandes o inestables, mostrando el límite de la estabilidad.

---

## 🧭 8. Valores de PID recomendados

| Objetivo             | Kp   | Ki       | Kd      |
|----------------------|------|----------|---------|
| Respuesta suave      | 2–4  | 0.3–0.7  | 0.1–0.4 |
| Respuesta más rápida | 4–6  | 0.5–1.0  | 0.2–0.8 |
| Control agresivo     | 6–10 | 1.0–2.0  | 0–0.3   |

Estos rangos son orientativos y se pueden ajustar para mostrar diferentes comportamientos al docente.

---

## 📂 9. Archivos incluidos

- **index.html** → Simulación completa (HTML + CSS + JS + Plotly).  
- **README.md** → Manual de usuario y documentación técnica.

