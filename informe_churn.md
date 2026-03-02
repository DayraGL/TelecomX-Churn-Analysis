# **Informe de Análisis de Evasión de Clientes (Churn) - TelecomX**

## Introducción

El presente informe tiene como objetivo analizar el comportamiento de los clientes de TelecomX para identificar los factores que influyen en la **evasión (churn)**. La deserción de clientes representa una pérdida significativa de ingresos y un desafío estratégico para la empresa. Mediante un proceso de extracción, limpieza y análisis exploratorio de datos (EDA), se busca comprender qué características diferencian a los clientes que abandonan el servicio de aquellos que permanecen, con el fin de proponer acciones basadas en datos para reducir la tasa de evasión.

## Limpieza y Tratamiento de Datos

Los datos fueron obtenidos desde una API pública en formato JSON y cargados en un DataFrame de Pandas. El dataset original contenía 7267 filas y 6 columnas, con variables anidadas en diccionarios. Se normalizaron estas columnas para obtener un total de 21 variables, incluyendo información demográfica, servicios contratados, tipo de contrato, método de pago y cargos.

**Pasos realizados:**

- **Extracción**: Se utilizó la librería `requests` para obtener los datos y se convirtieron a DataFrame.
- **Exploración inicial**: Se verificó la estructura, tipos de datos y valores nulos. No se encontraron nulos evidentes, pero se detectaron valores en blanco en la columna `account_Charges_Total` correspondientes a clientes con antigüedad cero, los cuales se imputaron con 0.
- **Estandarización**: Se renombraron columnas a nombres más descriptivos en español (ej. `Churn` → `evasion`, `customer_tenure` → `Meses_Permanencia`). Se mapearon variables binarias (`Yes`/`No`) a valores numéricos (1/0). Se manejaron valores como `'No internet service'` como 0 en las columnas de servicios adicionales.
- **Limpieza de valores nulos**: Se identificaron 707 valores nulos en `phone_MultipleLines` y columnas relacionadas con internet, los cuales fueron rellenados con 0 y convertidos a enteros, asumiendo que la ausencia de servicio implica "No".
- **Verificación final**: Se confirmó la ausencia de duplicados y nulos, y se guardó el dataset limpio en `TelecomX_Data.csv`.

## Análisis Exploratorio de Datos

Se realizaron diversos análisis univariados y bivariados para caracterizar la evasión. A continuación se presentan los principales hallazgos, respaldados por visualizaciones.


### **1. Variable objetivo: evasión**
- El **25.7%** de los clientes (1,869) ha desertado, mientras que el **74.3%** (5,398) permanece activo.
<img width="590" height="490" alt="image" src="https://github.com/user-attachments/assets/f4d7b9bf-9547-477f-be52-c1e281efad75" />

### **2. Género**
- Población equilibrada: 3,592 mujeres y 3,675 hombres.
- Tasa de evasión similar: **26.1%** en mujeres y **25.3%** en hombres. El género no es un factor determinante.

<img width="1389" height="490" alt="image" src="https://github.com/user-attachments/assets/98911365-5dc5-4d79-8c17-f605e3baf323" />


### **3. Tipo de contrato**
- **Contrato mensual**: 4,005 clientes (58.7% activos, **41.3% evadidos**). Es el de mayor riesgo.
- **Contrato a un año**: 1,519 clientes (89.1% activos, 10.9% evadidos).
- **Contrato a dos años**: 1,743 clientes (97.2% activos, solo 2.8% evadidos).
- La evasión se concentra fuertemente en los contratos de mes a mes.

<img width="1389" height="490" alt="image" src="https://github.com/user-attachments/assets/d2077094-63e8-4273-9f2e-ceccc2fa5852" />


### **4. Método de pago**
- **Cheque electrónico**: 1,357 clientes, con la mayor tasa de evasión: **43.8%**.
- **Cheque por correo**: 1,357 clientes, 18.5% evadidos.
- **Transferencia bancaria automática**: 1,331 clientes, 16.2% evadidos.
- **Tarjeta de crédito automática**: 1,336 clientes, 14.8% evadidos.
- Los métodos de pago automáticos presentan menor deserción.

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/db80b909-4692-4ab9-b65c-a909e9243ccb" />

<img width="1165" height="506" alt="image" src="https://github.com/user-attachments/assets/d3d8dcc0-8b71-46ba-a327-d08ce4a83de9" />

<img width="720" height="504" alt="image" src="https://github.com/user-attachments/assets/51177996-bf49-4d05-b58b-4196fc1f679e" />


### **5. Tipo de internet**
- **Fibra óptica**: 3,198 clientes (59.4% activos, **40.6% evadidos**). Es el servicio con mayor deserción.
- **DSL**: 2,488 clientes (81.6% activos, 18.4% evadidos).
- **Sin internet**: 1,581 clientes (92.9% activos, solo 7.1% evadidos).
- La fibra óptica, a pesar de ser el más usado, tiene una alta tasa de fuga.

<img width="1389" height="490" alt="image" src="https://github.com/user-attachments/assets/b04181c6-5997-4290-bd72-577c39013d93" />


### **6. Estado civil (En_Pareja)**
- **Solteros**: 3,749 clientes (2,549 activos, **1,200 evadidos**).
- **En pareja**: 3,518 clientes (2,849 activos, 669 evadidos).
- Los solteros desertan en mayor proporción (32% vs 19% de los que tienen pareja).

<img width="990" height="490" alt="image" src="https://github.com/user-attachments/assets/08121099-8032-4492-9532-246b92dc3276" />


### **7. Dependientes**
- **Sin dependientes**: 5,086 clientes (3,543 activos, **1,543 evadidos**).
- **Con dependientes**: 2,181 clientes (1,855 activos, 326 evadidos).
- Quienes tienen dependientes son más leales (solo 15% de evasión frente a 30% de los que no tienen).

<img width="989" height="490" alt="image" src="https://github.com/user-attachments/assets/03dfe227-9104-48ad-bb30-0bac1a60b662" />


### **8. Servicio telefónico**
- **Con servicio telefónico**: 6,560 clientes (4,861 activos, 1,699 evadidos).
- **Sin servicio telefónico**: 707 clientes (537 activos, 170 evadidos).
- La evasión es ligeramente mayor entre quienes tienen teléfono (25.9% vs 24.0%).

<img width="989" height="490" alt="image" src="https://github.com/user-attachments/assets/08fbf18e-9117-4e15-abbe-69c099a57084" />


### **9. Servicios adicionales de internet**
Se analizó la cantidad de servicios contratados (de 0 a 6) entre los siguientes: OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies.

- **Entre los que desertaron**:
  - 0 servicios: 25.4%
  - 1 servicio: 23.6%
  - 2 servicios: 19.8%
  - 3 servicios: 16.4%
  - 4 servicios: 10.2%
  - 5 servicios: 3.8%
  - 6 servicios: 0.8%
    
- **Entre los que permanecen**:
  - 0 servicios: 33.8%
  - 1 servicio: 10.2%
  - 2 servicios: 12.7%
  - 3 servicios: 15.6%
  - 4 servicios: 12.9%
  - 5 servicios: 9.6%
  - 6 servicios: 5.1%

**Observación**: Los desertores tienden a contratar menos servicios (especialmente los de seguridad y soporte). Mientras que los clientes que se quedan contratan más servicios, especialmente a partir de 3.

<img width="859" height="548" alt="image" src="https://github.com/user-attachments/assets/c85bf6ac-9f0a-4e4e-a2fe-9aa0d97068ac" />

<img width="982" height="590" alt="image" src="https://github.com/user-attachments/assets/cd44a7c2-03f5-4907-a8ce-da3c30c0f307" />

<img width="849" height="672" alt="image" src="https://github.com/user-attachments/assets/cbb87ad8-6600-4f8c-baf3-1f0f6a5013f5" />

<img width="1389" height="590" alt="image" src="https://github.com/user-attachments/assets/2f6060c9-6662-4ceb-a955-ca0ada1caf8f" />

### **10. Cargo mensual**
- Distribución general:
  - 0-30 USD: 23.6%
  - 30-60 USD: 17.8%
  - 60-90 USD: 33.8%
  - 90-120 USD: 24.8%
  
- Entre desertores:
  - 0-30: 8.7%
  - 30-60: 17.5%
  - 60-90: 43.2%
  - 90-120: 30.7%
  
- Entre activos:
  - 0-30: 28.7%
  - 30-60: 17.9%
  - 60-90: 30.6%
  - 90-120: 22.8%

**Correlación**: Existe una correlación positiva de **0.19** entre el cargo mensual y la evasión. Los desertores pagan en promedio **$74** mensuales, frente a **$61** de los activos (diferencia de $13). Esto indica que a mayor cargo, ligeramente mayor probabilidad de fuga, aunque no es el factor principal.

<img width="790" height="589" alt="image" src="https://github.com/user-attachments/assets/d718d920-c051-487a-88cb-511592f15944" />


### **11. Meses de permanencia**
- **Desertores**: mediana de **10 meses**. El 25% se fue antes de los 2 meses y el 75% antes de los 29 meses.
- **Activos**: mediana de **37 meses**. El 25% lleva más de 61 meses (5 años).
- La permanencia es el factor más diferenciador: los clientes nuevos tienen alto riesgo de fuga; superado el primer año, la lealtad aumenta significativamente.

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/6f8e79f4-d5b6-4832-8d62-fe150d3298c7" />


## Conclusiones e Insights

1. **El tipo de contrato es el factor más determinante**: los clientes con contrato mensual tienen una tasa de evasión del 41%, 15 veces superior a la de contratos a dos años.
2. **Los métodos de pago automáticos (tarjeta y transferencia) retienen mejor**: solo 15-16% de evasión, frente al 44% del cheque electrónico.
3. **La fibra óptica presenta alta deserción (41%)** a pesar de ser el servicio más contratado. Posible insatisfacción con la calidad o precio.
4. **Los clientes con pareja y/o dependientes son más leales**: la responsabilidad familiar parece aumentar la permanencia.
5. **La contratación de servicios adicionales (especialmente seguridad y soporte) se asocia con menor evasión**: los desertores usan menos estos servicios.
6. **El cargo mensual influye levemente**: los que pagan más tienden a irse un poco más, pero no es lo más relevante.
7. **La permanencia es clave**: el 50% de los desertores se va en los primeros 10 meses. El riesgo se concentra en clientes nuevos.

## Recomendaciones Estratégicas

1. **Fomentar contratos a largo plazo**: Ofrecer incentivos (descuentos, meses gratis, mejoras en servicios) para que clientes de contrato mensual migren a anual o bianual.
2. **Revisar la propuesta de valor de fibra óptica**: Realizar encuestas de satisfacción, mejorar la estabilidad del servicio y considerar promociones para retener a estos clientes.
3. **Promover métodos de pago automáticos**: Ofrecer pequeños descuentos por domiciliación bancaria o pago con tarjeta, y comunicar sus ventajas.
4. **Implementar un programa de bienvenida y acompañamiento**: Enfocar esfuerzos en los primeros 6-12 meses con seguimiento personalizado, ofertas y asistencia para reducir la fuga temprana.
5. **Incentivar la contratación de servicios de valor agregado**: Incluir en paquetes básicos servicios como seguridad online o soporte técnico, o crear bundles atractivos que aumenten la adherencia.
6. **Segmentar campañas de retención**: Dirigirse a clientes con perfil de alto riesgo: contrato mensual, pago con cheque electrónico, fibra óptica, baja antigüedad y sin servicios adicionales.
7. **Monitorear la evasión por cohortes**: Analizar periódicamente la deserción según mes de ingreso para evaluar el impacto de las acciones implementadas.

Este análisis proporciona una base sólida para la toma de decisiones orientadas a disminuir la deserción y aumentar la lealtad de los clientes de TelecomX. Se recomienda continuar con la construcción de un modelo predictivo que permita identificar clientes en riesgo de manera proactiva.
