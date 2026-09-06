# Telco Customer Churn
## Análisis Exploratorio de Datos para la comprensión del abandono de clientes

Este proyecto desarrolla un **Análisis Exploratorio de Datos (EDA)** sobre el conjunto de datos **Telco Customer Churn**, con el propósito de comprender la magnitud del abandono de clientes, evaluar la calidad de los datos e identificar patrones y segmentos asociados a `Churn`.

El análisis se aborda desde una perspectiva de negocio, buscando generar **hallazgos medibles, cuantificables y comunicables** que puedan apoyar futuras decisiones orientadas a la retención de clientes.

> **Alcance de esta entrega:** comprensión del problema, auditoría de calidad, preparación de datos, EDA, privacidad, ética y evaluación de posibles sesgos.  
> **No se realiza entrenamiento de modelos de Machine Learning en esta etapa.**

---

## 1. Problema de negocio

El abandono de clientes (*customer churn*) representa una problemática relevante para una empresa de telecomunicaciones, ya que corresponde a clientes que dejan de utilizar los servicios de la compañía.

Comprender qué características presentan los clientes que abandonan resulta relevante para orientar futuras estrategias de retención y priorizar segmentos que requieran mayor atención.

El conjunto de datos contiene información demográfica, servicios contratados, características de la relación comercial, métodos de pago, cargos y la variable `Churn`, que indica si un cliente abandonó (`Yes`) o permaneció (`No`) en la compañía.

La pregunta principal que orienta el análisis es:

> **¿Qué características y segmentos presentan diferencias relevantes en la tasa de abandono dentro del conjunto de datos Telco Customer Churn?**

El análisis busca identificar **asociaciones exploratorias**, no establecer relaciones causales.

---

## 2. Objetivos

### 2.1 Objetivo general

Realizar un análisis exploratorio sobre los **7.043 registros** del conjunto de datos Telco Customer Churn, cuantificando la magnitud del abandono, evaluando la calidad y consistencia de los datos e identificando patrones y segmentos con diferencias relevantes en `Churn`, con el propósito de generar hallazgos que apoyen futuras decisiones de retención de clientes.

### 2.2 Objetivos específicos

- Caracterizar la estructura y composición del conjunto de datos.
- Evaluar la completitud, unicidad, validez y consistencia de los datos.
- Identificar y justificar el tratamiento de anomalías detectadas durante la auditoría de calidad.
- Cuantificar la tasa global de abandono de clientes.
- Analizar diferencias en `Churn` según características comerciales y de permanencia.
- Profundizar los hallazgos mediante análisis multivariados que eviten interpretaciones aisladas de las variables.
- Identificar segmentos con tasas de abandono superiores al comportamiento global.
- Evaluar aspectos de privacidad, anonimización, ética y posibles sesgos.
- Generar hallazgos cuantificados y comunicables orientados a la comprensión del problema de negocio.

---

## 3. Indicadores clave de desempeño (KPIs)

Para cuantificar el problema de abandono se consideran los siguientes indicadores:

| KPI | Resultado |
|---|---:|
| Total de clientes analizados | 7.043 |
| Clientes que abandonan | 1.869 |
| Clientes que permanecen | 5.174 |
| Tasa global de abandono | 26,54 % |
| Tasa global de permanencia | 73,46 % |

La **tasa global de abandono (26,54 %)** se utiliza como referencia interna para comparar el comportamiento de distintos segmentos del conjunto de datos.

---

## 4. Fuente y descripción de los datos

El proyecto utiliza el conjunto de datos **Telco Customer Churn**, compuesto por **7.043 observaciones y 21 variables** en su versión original.

Cada registro representa un cliente e incorpora información relacionada con:

- características demográficas y personales;
- antigüedad del cliente (`tenure`);
- servicios contratados;
- tipo de contrato;
- método de pago;
- cargos mensuales y acumulados;
- condición de abandono (`Churn`).

La variable objetivo del análisis es `Churn`:

- `Yes`: el cliente presenta abandono.
- `No`: el cliente permanece.

> **Fuente del dataset:** https://github.com/eduardodrm/machine_learning_ev1/blob/main/data/Telco_Customer_Churn_Dataset.csv

---

## 5. Metodología CRISP-DM

El proyecto utiliza **CRISP-DM (Cross-Industry Standard Process for Data Mining)** como marco metodológico para estructurar el proceso de trabajo.

De acuerdo con el alcance de esta evaluación, se desarrollan principalmente las siguientes etapas:

### 5.1 Business Understanding

Se define el problema de negocio asociado al abandono de clientes, estableciendo como foco del análisis la variable `Churn` y orientando el proyecto hacia la generación de hallazgos útiles para futuras decisiones de retención.

### 5.2 Data Understanding

Se realiza una comprensión progresiva del conjunto de datos mediante:

- revisión de dimensiones y variables;
- análisis de tipos de datos;
- estadística descriptiva;
- evaluación de calidad;
- análisis univariado y bivariado;
- profundización mediante cruces multivariados.

Esta etapa permitió identificar patrones, inconsistencias y relaciones que posteriormente orientaron las decisiones de preparación.

### 5.3 Data Preparation

Las transformaciones se realizan únicamente cuando existe evidencia que justifica una intervención.

Entre las principales acciones se encuentran:

- investigación y tratamiento de 11 registros con espacios en blanco en `TotalCharges`;
- conversión de `TotalCharges` desde `object` a tipo numérico;
- imputación condicionada de los 11 casos asociados a `tenure = 0`;
- exclusión de `customerID` en la versión preparada por corresponder a un identificador único no necesario para posteriores propósitos analíticos;
- validación final de valores ausentes, duplicados y estructura del conjunto preparado.

### Etapas fuera del alcance

Las etapas de **Modeling**, **Evaluation** y **Deployment** forman parte de CRISP-DM, pero no se desarrollan en esta evaluación debido a que el alcance corresponde al análisis exploratorio, preparación y evaluación responsable de los datos.

---

## 6. Auditoría y preparación de los datos

### 6.1 Completitud

La revisión inicial mediante funciones de detección de nulos no identificó valores ausentes reconocidos automáticamente por Pandas.

Sin embargo, una inspección adicional de `TotalCharges` permitió detectar **11 registros representados mediante espacios en blanco**. Estos valores no eran reconocidos inicialmente como `NaN` y provocaban que la variable estuviera almacenada como `object` pese a representar un monto.

Los 11 registros afectados presentaban `tenure = 0`.

### 6.2 Unicidad

- No se identificaron registros completamente duplicados.
- `customerID` presenta **7.043 valores únicos para 7.043 observaciones**.
- No se identificaron identificadores repetidos.

### 6.3 Validez y consistencia

Se revisaron categorías, rangos y relaciones lógicas entre variables.

Entre las validaciones realizadas se incluyeron:

- codificación binaria de `SeniorCitizen`;
- categorías válidas de `Churn` y `Contract`;
- rangos no negativos en `tenure`, `MonthlyCharges` y `TotalCharges`;
- consistencia entre `PhoneService` y `MultipleLines`;
- consistencia entre `InternetService` y los servicios dependientes de Internet.

Categorías como `No internet service` y `No phone service` fueron interpretadas como **situaciones válidas de no aplicabilidad**, no como valores ausentes.

### 6.4 Tratamiento de `TotalCharges`

La variable se convirtió a formato numérico, haciendo explícitos como `NaN` los valores que no podían convertirse.

Posteriormente, los 11 valores ausentes fueron imputados con `0` **únicamente cuando `tenure = 0`**, evitando una imputación indiscriminada.

Después del tratamiento:

- `TotalCharges` quedó almacenada como variable numérica;
- no quedaron valores ausentes en la variable;
- se mantuvieron las 7.043 observaciones originales.

### 6.5 Identificador único

`customerID` fue utilizado durante la auditoría para verificar la unicidad de los registros.

Posteriormente se excluyó de la versión preparada del dataset debido a que:

- corresponde a un identificador individual;
- no representa una característica del comportamiento del cliente;
- su exclusión responde a un criterio de minimización de datos.

La versión preparada contiene **7.043 observaciones y 20 variables**.

Tras excluir `customerID`, Pandas identifica **22 filas repetidas respecto de una observación previa** en la versión preparada. Al revisar estos casos se observa que corresponden a **42 clientes distribuidos en 20 perfiles idénticos** sobre las 20 variables restantes. Debido a que el dataset original presenta 7.043 `customerID` únicos y ningún registro completamente duplicado, estos casos no se interpretan como clientes duplicados, sino como clientes distintos que comparten exactamente el mismo perfil analítico. Por esta razón, **se mantienen en el conjunto de datos**.

---

## 7. Análisis exploratorio de datos

El EDA se desarrolló de forma progresiva, comenzando por el comportamiento general de `Churn` y profundizando posteriormente en relaciones bivariadas y multivariadas.

Las principales dimensiones analizadas fueron:

- magnitud global del abandono;
- permanencia del cliente (`tenure`);
- tipo de contrato (`Contract`);
- cargos mensuales (`MonthlyCharges`);
- servicio de Internet (`InternetService`);
- método de pago (`PaymentMethod`);
- relación conjunta entre contrato, permanencia y abandono;
- relación conjunta entre servicio de Internet, cargos mensuales y abandono;
- comportamiento de variables personales relevantes desde una perspectiva ética.

Las visualizaciones se diseñaron con un enfoque ejecutivo, priorizando títulos comunicacionales, resultados cuantificados, comparación mediante tasas y proporciones y una interpretación orientada al negocio.

---

## 8. Hallazgos principales

### 8.1 Aproximadamente 1 de cada 4 clientes presenta abandono

De los **7.043 clientes analizados**, **1.869 presentan `Churn = Yes`**, equivalente a una tasa global de aproximadamente **26,54 %**.

### 8.2 El mayor abandono se concentra en clientes nuevos con contrato mensual

El análisis conjunto de `Contract`, `tenure` y `Churn` identificó al segmento de clientes con **contrato mensual y hasta 9 meses de permanencia** como el de mayor tasa de abandono entre los segmentos analizados.

En este grupo:

- Clientes: **1.732**
- Abandonos: **916**
- Tasa de abandono: **52,89 %**

Dentro de los contratos mensuales, la tasa de abandono disminuye progresivamente a medida que aumenta la permanencia:

| Permanencia | Tasa de abandono |
|---|---:|
| 0–9 meses | 52,89 % |
| 10–29 meses | 37,46 % |
| 30–55 meses | 32,83 % |
| 56–72 meses | 22,05 % |

Este resultado muestra que `tenure` y `Contract` no deben interpretarse de manera aislada.

### 8.3 La fibra óptica presenta una elevada tasa de abandono

Los clientes con **fibra óptica** presentan una tasa de abandono aproximada de **41,89 %**, superior al **26,54 % global**.

| Servicio | Tasa de abandono |
|---|---:|
| Fibra óptica | 41,89 % |
| DSL | 18,96 % |
| Sin Internet | 7,40 % |

Además, aproximadamente **69,40 % de los clientes que abandonan utiliza fibra óptica**.

### 8.4 Los cargos mensuales no deben interpretarse de forma aislada

En el análisis agregado:

- Mediana `MonthlyCharges` entre quienes abandonan: **79,65**
- Mediana `MonthlyCharges` entre quienes permanecen: **64,43**

Sin embargo, al comparar clientes dentro del mismo tipo de servicio de Internet, esta diferencia no se mantiene:

| Servicio | Permanece | Abandona |
|---|---:|---:|
| Sin Internet | 20,15 | 20,00 |
| DSL | 59,75 | 49,25 |
| Fibra óptica | 94,80 | 87,55 |

La mayor mediana global observada inicialmente entre quienes abandonan está influenciada por la elevada concentración de clientes con fibra óptica dentro de este grupo.

Este hallazgo evidencia la importancia de **profundizar el EDA antes de interpretar variables de manera independiente**.

### 8.5 El cheque electrónico presenta la mayor tasa de abandono entre los métodos de pago

Los clientes que utilizan **cheque electrónico** presentan una tasa de abandono aproximada de **45,29 %**.

| Método de pago | Tasa de abandono |
|---|---:|
| Cheque electrónico | 45,29 % |
| Cheque por correo | 19,11 % |
| Transferencia automática | 16,71 % |
| Tarjeta automática | 15,24 % |

La tasa de cheque electrónico supera en aproximadamente **18,75 puntos porcentuales** la tasa global del dataset.

### 8.6 `SeniorCitizen` requiere una interpretación contextual y ética

Los clientes clasificados como `SeniorCitizen = 1` presentan una tasa de abandono aproximada de **41,68 %**, frente a **23,61 %** en `SeniorCitizen = 0`.

Sin embargo, el grupo `SeniorCitizen = 1` también presenta una mayor concentración de características previamente asociadas con tasas elevadas de abandono:

| Característica | SeniorCitizen = 0 | SeniorCitizen = 1 |
|---|---:|---:|
| Contrato mensual | 51,99 % | 70,67 % |
| Fibra óptica | 38,38 % | 72,77 % |
| Cheque electrónico | 30,01 % | 52,01 % |
| Mediana MonthlyCharges | 65,80 | 84,85 |

Por lo tanto, la mayor tasa de abandono observada no debe atribuirse directamente a la condición representada por `SeniorCitizen`.

---

## 9. Ética, privacidad y posibles sesgos

### 9.1 Representatividad

La variable `gender` presenta una representación prácticamente equilibrada:

- Female: **49,52 %**
- Male: **50,48 %**

Las tasas de abandono observadas también son similares:

- Female: **26,92 %**
- Male: **26,16 %**

En este análisis descriptivo no se observa una diferencia relevante entre ambas categorías. Sin embargo, esto no permite afirmar ausencia total de sesgo en otros cruces o en un eventual modelo.

### 9.2 Variables personales

Variables como `gender` y `SeniorCitizen` requieren especial precaución debido a que representan características personales.

Una diferencia estadística entre grupos no implica que dicha característica sea la causa del abandono ni justifica decisiones perjudiciales hacia un segmento.

### 9.3 Privacidad y minimización

El conjunto de datos no contiene identificadores personales directos como nombre, correo, teléfono o dirección.

Sin embargo, `customerID` corresponde a un identificador único y fue excluido de la versión preparada siguiendo un criterio de **minimización de datos**.

Su eliminación reduce el uso de identificadores innecesarios, pero no permite afirmar que el conjunto de datos se encuentre completamente anonimizado.

### 9.4 Anonimización y pseudonimización

La eliminación de un identificador no garantiza por sí sola anonimización irreversible.

En un entorno real, la combinación de diversas características podría contribuir a la reidentificación si existiera información externa adicional.

Por esta razón, un proyecto productivo debería considerar controles de acceso, minimización, anonimización o pseudonimización según el nivel de riesgo y propósito del tratamiento.

### 9.5 Uso responsable futuro

En una eventual etapa de modelamiento sería necesario:

- evaluar cuidadosamente el uso de variables personales;
- comprobar representatividad entre grupos;
- evaluar diferencias sistemáticas en resultados futuros;
- evitar interpretaciones causales a partir de asociaciones exploratorias;
- utilizar únicamente información necesaria para el propósito del proyecto;
- proteger el acceso a la información;
- orientar las decisiones hacia acciones beneficiosas para los clientes y evitar prácticas discriminatorias.

---

## 10. Limitaciones

Los resultados corresponden exclusivamente al conjunto de datos analizado y deben interpretarse dentro de dicho contexto.

El dataset no entrega información suficiente para establecer relaciones causales entre las características de los clientes y el abandono.

Tampoco se dispone, dentro del alcance actual, de información adicional sobre:

- contexto temporal detallado;
- políticas comerciales de la empresa;
- satisfacción del cliente;
- calidad efectiva del servicio;
- interacciones con soporte;
- campañas comerciales;
- factores externos que puedan influir en la decisión de abandonar.

Por esta razón, los hallazgos deben considerarse **asociaciones exploratorias útiles para orientar investigaciones y decisiones posteriores**, no evidencia definitiva de causalidad.

---

## 11. Herramientas y colaboración

El proyecto utiliza las siguientes herramientas:

- **Python / Pandas:** manipulación, auditoría y análisis de datos.
- **Plotly:** visualizaciones interactivas orientadas al EDA y comunicación de hallazgos.
- **Google Colab:** desarrollo y ejecución reproducible del notebook.
- **Git y GitHub:** centralización del proyecto, control de versiones, trazabilidad de cambios y colaboración entre integrantes.

GitHub se utiliza como repositorio central para mantener una estructura organizada del proyecto, registrar cambios y facilitar la reproducibilidad del análisis.

---

## 12. Estructura del repositorio

```text
machine_learning_ev1/
│
├── data/
│   ├── raw/
│   │   └── Telco_Customer_Churn_Dataset.csv
│   │
│   └── processed/
│       └── telco_customer_churn_processed.csv
│
├── images/
│
├── models/
│
├── notebooks/
│   └── EV1_ML_Analisis_Exploratorio_Abandono_Clientes.ipynb
│
└── README.md

```

- `README.md`: documentación principal del proyecto.
- `data/raw/`: conjunto de datos original sin modificaciones.
- `data/processed/`: versión preparada después de las transformaciones justificadas.
- `notebooks/`: notebook reproducible con el proceso completo de auditoría, preparación y EDA.
- `images/`: recursos gráficos utilizados en documentación o presentación, cuando corresponda.

---

## 13. Reproducibilidad

El notebook documenta de manera secuencial el proceso necesario para reproducir el análisis:

1. importación de librerías;
2. carga del dataset original;
3. comprensión inicial;
4. auditoría de calidad;
5. tratamiento justificado de inconsistencias;
6. análisis estadístico descriptivo;
7. EDA bivariado y multivariado;
8. evaluación de privacidad, ética y posibles sesgos;
9. creación del conjunto de datos preparado;
10. exportación del archivo procesado.

El archivo original se mantiene sin modificaciones en `data/raw/`, mientras que las transformaciones se generan mediante código y se almacenan separadamente en `data/processed/`.

---

## 14. Conclusiones

El análisis exploratorio permitió determinar que el abandono de clientes **no se distribuye uniformemente** dentro del conjunto de datos.

La tasa global de `Churn` alcanza aproximadamente **26,54 %**, pero determinados segmentos presentan comportamientos considerablemente diferentes.

El hallazgo más relevante corresponde a los clientes con **contrato mensual y hasta 9 meses de permanencia**, cuya tasa de abandono alcanza aproximadamente **52,89 %**, prácticamente el doble de la tasa global.

También se identificaron tasas elevadas de abandono entre clientes con fibra óptica y cheque electrónico.

La profundización multivariada demostró además la importancia de no interpretar variables de manera aislada. En particular, la mayor presencia de cargos mensuales entre quienes abandonan se encuentra influenciada por la elevada concentración de clientes con fibra óptica dentro de este grupo.

Desde la perspectiva de calidad, las transformaciones se realizaron únicamente cuando existió evidencia que justificara una intervención, manteniendo la trazabilidad de las decisiones.

Finalmente, el análisis de privacidad y posibles sesgos evidencia la necesidad de utilizar con precaución variables personales y aplicar principios de minimización de datos antes de una eventual continuación del proyecto hacia etapas de modelamiento.

> **Conclusión general:** el EDA no busca únicamente describir los datos, sino comprender cómo se relacionan sus características, cuestionar interpretaciones iniciales y generar evidencia suficientemente contextualizada para apoyar decisiones posteriores.
