# Análisis Inferencial y Modelado Predictivo de Salud e IMC

Proyecto de análisis estadístico aplicado, pruebas de hipótesis paramétricas y optimización de un modelo de regresión lineal múltiple (OLS) para la estimación del **Índice de Masa Corporal (IMC)** a partir de hábitos y factores demográficos en adultos.

---

## 📌 Contexto del Dataset

El conjunto de datos analiza métricas de salud y actividad física de una muestra de participantes adultos:
* **Edad:** Participantes entre 18 y 70 años.
* **HorasEjercicio:** Horas dedicadas a actividad física semanal.
* **ConsumoCalorias:** Ingesta calórica diaria reportada (1500 a 3500 kcal).
* **IMC:** Índice de Masa Corporal (variable objetivo dependiente).
* **Variables complementarias:** Género, Nivel de Actividad y Región.

> **Nota sobre los datos:**  
> Por motivos de confidencialidad y origen académico, el archivo fuente `Data_Examen.xlsx` no se distribuye de forma pública en este repositorio. La totalidad de las salidas de ejecución (`head()`, `describe()`), resúmenes estadísticos (`summary()`) y gráficos se encuentran completamente generados y visibles dentro del archivo interactivo `.ipynb`.

---

## 🛠️ Stack Tecnológico

* **Lenguaje:** Python
* **Manipulación de Datos:** `pandas`, `numpy`
* **Inferencia Estadística:** `scipy.stats` (T-test unilateral, correlación de Pearson, prueba de normalidad de Shapiro-Wilk)
* **Modelado Predictivo:** `statsmodels.api` (Mínimos Cuadrados Ordinarios - OLS)
* **Visualización:** `matplotlib`, `seaborn`

---

## 🔍 Metodología y Resultados

### 1. Inferencia sobre Hábitos de Ejercicio Físico (T-Test Unilateral)
* **Hipótesis:** Se contrastó si la media poblacional de horas de ejercicio semanal es significativamente menor a 8 horas ($H_0: \mu \ge 8$ vs. $H_1: \mu < 8$).
* **Resultado:** Con un estadístico observado $t = -0,32$ y un $p\text{-valor}$ unilateral de $0,37$ ($> 0,05$), **no se rechaza la hipótesis nula**. No existe evidencia estadística suficiente para afirmar que los participantes promedian menos de 8 horas semanales de ejercicio.

### 2. Correlación Bivariada (Pearson)
* **Evaluación:** Grado de asociación lineal entre la edad de los participantes y el IMC ($H_0: \rho = 0$ vs. $H_1: \rho \ne 0$).
* **Resultado:** Se obtuvo un coeficiente estadísticamente significativo con $p\text{-valor} < 0,001$, rechazando la hipótesis nula. Se confirma la existencia de una correlación lineal positiva entre ambas variables.

### 3. Modelado Predictivo y Selección de Variables (Regresión Múltiple OLS)
* **Modelo Inicial:** Se estimó el modelo completo incorporando `Edad`, `HorasEjercicio` y `ConsumoCalorias`, alcanzando un coeficiente de determinación $R^2 = 0,9293$.
* **Evaluación de Significancia Individual:**  
  * `Edad`: $p < 0,001$ (significativa).  
  * `HorasEjercicio`: $p < 0,001$ (significativa).  
  * `ConsumoCalorias`: $p = 0,671$ (no significativa, $p > 0,05$).
* **Modelo Parsimonioso Optimizado:**  
  Tras remover la variable no significativa, la ecuación resultante fue:
  $$\text{IMC} = -0,09 + 0,25 \times \text{Edad} - 0,15 \times \text{HorasEjercicio}$$
  * Por cada año adicional de edad, el IMC estimado se incrementa en promedio **0,25 unidades** (*ceteris paribus*).
  * Por cada hora extra de ejercicio semanal, el IMC estimado se reduce en promedio **0,15 unidades**.
  * El nuevo modelo mantiene un $R^2 = 0,9292$, conservando el poder explicativo con una estructura más eficiente.

### 4. Validación de Supuestos de Residuos (Shapiro-Wilk)
* **Evaluación:** Contraste de normalidad de los residuos del modelo de regresión ($H_0: \text{Residuos normales}$ vs. $H_1: \text{Residuos no normales}$).
* **Resultado:** Con un estadístico $W = 0,99$ y un $p\text{-valor} = 0,77$ ($> 0,05$), no se rechaza la hipótesis nula, validando formalmente el supuesto de normalidad en las perturbaciones del modelo.

---

## 💻 Visualización del Proyecto

Para explorar el desarrollo completo del código, las celdas ejecutadas y las interpretaciones:
* Abre el archivo interactivo `.ipynb` directamente en el visor de GitHub o mediante el botón de Google Colab integrado.
