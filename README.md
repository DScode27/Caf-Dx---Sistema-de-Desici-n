# ☕ CaféDx — Diagnóstico Bayesiano de Cultivos de Café

Sistema de diagnóstico de enfermedades en cultivos de café basado en **Teoría Bayesiana de la Decisión**, con agente de inteligencia artificial integrado.

> Proyecto Final — Investigación de Operaciones · Grupo 4 · Tema: Teoría Bayesiana de la Decisión

---

## ¿Qué hace?

El agricultor ingresa cinco evidencias visuales y ambientales de su cultivo. El sistema aplica el **Teorema de Bayes** para calcular la probabilidad posterior de cuatro condiciones (roya, antracnosis, broca y deficiencia nutricional), evalúa la **función de pérdida esperada** para cada posible tratamiento, y recomienda la decisión óptima $D^*$ que minimiza el costo esperado.

Un **agente de IA** (Gemini 2.5 Flash) interpreta los resultados en lenguaje natural y responde preguntas del usuario sobre el diagnóstico.

---

## Estructura del proyecto

```
cafedx/
├── index.html          # Página principal: formulario + modelo + agente IA
├── configuracion.html  # Editor de parámetros del modelo
├── styles.css          # Estilos página principal
└── stylesConf.css      # Estilos página de configuración
```

---

## Evidencias del modelo

| # | Variable | Opciones |
|---|---|---|
| E₁ | Color de hojas | Normal, Amarillo, Manchas naranjas, Manchas oscuras |
| E₂ | Estado de frutos | Normal, Con perforaciones, Momificados, Decolorados |
| E₃ | Patrón de afectación | Plantas aisladas, Por filas, Toda el área |
| E₄ | Humedad reciente | Baja, Media, Alta |
| E₅ | Parte afectada | Solo hojas, Solo frutos, Hojas y tallos, General |

---

## Uso

1. Abrir `index.html` en el navegador
2. Seleccionar las cinco evidencias observadas en el cultivo
3. Hacer clic en **Diagnosticar cultivo**
4. Revisar las probabilidades posteriores, la tabla de pérdida esperada y la decisión óptima
5. Usar el chat del agente IA para hacer preguntas sobre el diagnóstico

Para ajustar los parámetros del modelo (probabilidades previas, verosimilitudes, costos, función de pérdida), ir a **⚙ Configurar modelo**.

> Los cambios se guardan en `localStorage` y se aplican automáticamente al siguiente diagnóstico.

---

## Configuración del agente IA

El agente usa la API de Google Gemini. Para activarlo, reemplazar la constante `API_KEY` en `index.html` con tu clave de [Google AI Studio](https://aistudio.google.com/):

```js
const API_KEY = 'TU_API_KEY_AQUI';
```

---

## Tecnologías

- HTML · CSS · JavaScript vanilla
- [Google Gemini API](https://ai.google.dev/) vía `@google/genai`
- `localStorage` para persistencia de parámetros

---

## Modelo matemático

$$P(H_j \mid \mathbf{E}) = \frac{P(H_j)\prod_{i=1}^{5}P(E_i \mid H_j)}{\sum_{k}P(H_k)\prod_{i=1}^{5}P(E_i \mid H_k)}$$

$$D^* = \arg\min_{D_i} \sum_{j=1}^{4} L(D_i, H_j)\cdot P(H_j \mid \mathbf{E})$$
