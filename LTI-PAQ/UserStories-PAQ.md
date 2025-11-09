# Historias de Usuario — ATS LTI

Este documento contiene las 20 historias de usuario definidas para el MVP del sistema ATS LTI.  
Se agrupan en tres categorías: **funcionales (10)**, **técnicas (7)** e **integración (3)**.

---

## 🧩 I. Historias Funcionales (10)

### 1️⃣ Publicación de Vacantes
**Historia:**  
Como *recruiter*, quiero publicar una vacante en múltiples portales desde una sola pantalla, para ahorrar tiempo y mantener la consistencia de la información.  
**Criterios de aceptación:**  
- [ ] Se permite seleccionar plataformas (LinkedIn, Computrabajo, Bumeran).  
- [ ] El sistema confirma publicación exitosa o error.  
- [ ] El registro queda auditado con fecha, hora y usuario.  
**Relevancia:** Alta  

---

### 2️⃣ Anonimización de Candidatos
**Historia:**  
Como *recruiter*, quiero ver los candidatos sin mostrar sus datos personales, para evaluar de forma imparcial y reducir sesgos.  
**Criterios de aceptación:**  
- [ ] Se ocultan nombre, género, edad y contacto.  
- [ ] Se muestra identificador anónimo y puntaje IA.  
- [ ] Configurable por etapa del proceso.  
**Relevancia:** Alta  

---

### 3️⃣ Evaluación Colaborativa
**Historia:**  
Como *manager*, quiero poder dejar comentarios en los candidatos y ver los de otros evaluadores, para tomar decisiones consensuadas.  
**Criterios de aceptación:**  
- [ ] Comentarios versionados y visibles por equipo asignado.  
- [ ] Se registra usuario y fecha en cada comentario.  
- [ ] Auditado en tabla de cambios.  

---

### 4️⃣ Notificaciones de Progreso
**Historia:**  
Como *recruiter*, quiero recibir alertas cuando un candidato cambia de etapa, para mantener seguimiento sin revisar manualmente.  
**Criterios de aceptación:**  
- [ ] Notificaciones vía correo o Teams.  
- [ ] Configuración de frecuencia por usuario.  
- [ ] Registro de envío en logs.  

---

### 5️⃣ Registro de Actividad
**Historia:**  
Como *administrador de HR*, quiero acceder a un historial completo de todas las acciones de usuario, para auditar cumplimiento de políticas.  
**Criterios de aceptación:**  
- [ ] Logs por tenant, usuario, acción y fecha.  
- [ ] Exportable a CSV o API segura.  
- [ ] Retención mínima 90 días.  

---

### 6️⃣ Seguimiento de Ofertas
**Historia:**  
Como *recruiter*, quiero ver el estado de las ofertas enviadas y firmadas, para saber qué candidatos están próximos a incorporarse.  
**Criterios de aceptación:**  
- [ ] Estados: Enviada, En revisión, Firmada, Rechazada.  
- [ ] Actualización automática desde e-sign.  
- [ ] Notificación de cambio de estado.  

---

### 7️⃣ Panel de Candidatos por Vacante
**Historia:**  
Como *manager*, quiero visualizar en una sola vista todos los candidatos asociados a mi vacante, ordenados por score y etapa.  
**Criterios de aceptación:**  
- [ ] Vista filtrable por etapa y puntuación.  
- [ ] Sin datos personales visibles en etapas iniciales.  
- [ ] Sincronización en tiempo real.  

---

### 8️⃣ Consentimiento de Datos
**Historia:**  
Como *candidato*, quiero aceptar o rechazar el uso de mis datos personales antes de aplicar, para cumplir con las políticas de privacidad.  
**Criterios de aceptación:**  
- [ ] Checkbox obligatorio con enlace a política de privacidad.  
- [ ] Registro en tabla Consent con timestamp.  
- [ ] Aplicación bloqueada si no acepta.  

---

### 9️⃣ Acceso Seguro
**Historia:**  
Como *usuario*, quiero poder ingresar al sistema mediante Azure AD, para garantizar autenticación segura y centralizada.  
**Criterios de aceptación:**  
- [ ] Login mediante SSO.  
- [ ] Roles asignados por grupo de AD.  
- [ ] Registro de inicio y cierre de sesión.  

---

### 🔟 Filtros Avanzados de Candidatos
**Historia:**  
Como *recruiter*, quiero filtrar candidatos por skills, experiencia y disponibilidad, para optimizar mis búsquedas.  
**Criterios de aceptación:**  
- [ ] Filtros combinables por campo.  
- [ ] Resultado anónimo hasta etapa “Finalista”.  
- [ ] Guardado de filtros frecuentes.  

---

## ⚙️ II. Historias Técnicas (7)

### 1️⃣ Centralización de Logs
**Historia Técnica:**  
Como *devops*, quiero centralizar todos los logs de los microservicios en Azure Application Insights para un monitoreo unificado.  
**Criterios de aceptación:**  
- [ ] Envío estructurado (JSON) por servicio.  
- [ ] Filtros por tenant y módulo.  
- [ ] Retención mínima de 90 días.  

---

### 2️⃣ Monitoreo de Salud del Sistema
**Historia Técnica:**  
Como *administrador*, quiero un endpoint `/health` por servicio para validar disponibilidad desde Azure Monitor.  
**Criterios de aceptación:**  
- [ ] Respuesta HTTP 200 + JSON de estado.  
- [ ] Integrado a alertas en Azure Monitor.  
- [ ] Simulación de falla controlada.  

---

### 3️⃣ Auditoría de Acceso a Datos
**Historia Técnica:**  
Como *auditor interno*, quiero registrar quién consulta o modifica información sensible, para asegurar cumplimiento de políticas.  
**Criterios de aceptación:**  
- [ ] Registro de usuario, acción, entidad y timestamp.  
- [ ] Acceso restringido a rol “Auditor”.  
- [ ] Exportable a CSV cifrado.  

---

### 4️⃣ Encriptación de Campos Sensibles
**Historia Técnica:**  
Como *ingeniero de datos*, quiero almacenar los campos PII con Always Encrypted, para cumplir normativas de privacidad.  
**Criterios de aceptación:**  
- [ ] Columnas con CEK1 y algoritmo AES-256.  
- [ ] Pruebas de búsqueda determinística.  
- [ ] Acceso solo desde servicio autorizado.  

---

### 5️⃣ Orquestación de Eventos Fallidos
**Historia Técnica:**  
Como *orchestrator*, quiero reintentar eventos fallidos de publicación hasta 3 veces, para asegurar entrega confiable.  
**Criterios de aceptación:**  
- [ ] Reintento exponencial 1-3-9 min.  
- [ ] Log de errores persistente.  
- [ ] Notificación a administrador.  

---

### 6️⃣ Feature Flag de Anonimización
**Historia Técnica:**  
Como *admin de producto*, quiero activar o desactivar la anonimización por etapa desde configuración central, para facilitar pruebas.  
**Criterios de aceptación:**  
- [ ] Flag en tabla `FeatureFlags`.  
- [ ] Cambio en tiempo real.  
- [ ] Auditoría de modificaciones.  

---

### 7️⃣ Métricas de Performance
**Historia Técnica:**  
Como *devops*, quiero registrar métricas de tiempos promedio por endpoint, para identificar cuellos de botella.  
**Criterios de aceptación:**  
- [ ] Métricas en Azure Monitor.  
- [ ] Alertas si latencia > 2 seg.  
- [ ] Dashboard por microservicio.  

---

## 🔗 III. Historias de Integración (3)

### 1️⃣ Conector e-Sign
**Historia de Integración:**  
Como *recruiter*, quiero que el sistema envíe las ofertas a DocuSign automáticamente para firma digital.  
**Criterios de aceptación:**  
- [ ] API validada con sandbox.  
- [ ] Estado sincronizado cada 10 min.  
- [ ] Registro de EnvelopeId en base.  

---

### 2️⃣ Integración Outlook/Teams
**Historia de Integración:**  
Como *recruiter*, quiero que las entrevistas se sincronicen con el calendario Outlook y se creen reuniones Teams.  
**Criterios de aceptación:**  
- [ ] Invitación automática por Graph API.  
- [ ] Actualización bidireccional (cancelación/reprogramación).  
- [ ] Log de evento en tabla AuditLog.  

---

### 3️⃣ Conector HRIS
**Historia de Integración:**  
Como *sistema HRIS*, quiero recibir automáticamente los candidatos contratados desde ATS LTI, para crear su perfil de empleado.  
**Criterios de aceptación:**  
- [ ] Evento “Offer.Signed” publicado.  
- [ ] Reintento ante error (3 veces).  
- [ ] Confirmación de recepción registrada.  

---

# BACKLOG

ID	Descripción							Resultado

F2	Anonimización de Candidatos			sprint 1
F8	Consentimiento de Datos				sprint 1
F10	Filtros Avanzados					sprint 1
T3	Auditoría de Acceso a Datos			sprint 1
F1	Publicación de Vacantes				sprint 1
T4	Encriptación de Campos Sensibles	sprint 1

F5	Registro de Actividad				sprint 2
I1	Conector e-Sign						sprint 2
I3	Conector HRIS						sprint 2
T1	Centralización de Logs				sprint 2
T2	Monitoreo de Salud					sprint 2
T5	Orquestación de Eventos Fallidos	sprint 2
F3	Evaluación Colaborativa				sprint 2
I2	Integración Outlook/Teams			sprint 2

F4	Notificaciones de Progreso			sprint 3
F6	Seguimiento de Ofertas				sprint 3
T7	Métricas de Performance				sprint 3
F7	Panel de Candidatos					sprint 3
F9	Acceso Seguro (SSO)					sprint 3

T6	Feature Flag de Anonimización		sprint 4

La decisión se tomó combinando las 5 metodologías utilizadas para la generación de backlogs, donde hubo por lo general un mismo sprint asignado, o con una variante de un nivel.

ID	FINAL		Hibrido	Kano Model	WSJF	RICE	MoSCoW	Descripción
F2	sprint 1		F2	F2		F2	F2		F2		Anonimización de Candidatos
F8	sprint 1		F8	F8		F8	F8		F8		Consentimiento de Datos
F10	sprint 1		F9	F9		F9	F9		F9		Filtros Avanzados
T3	sprint 1		T3	T3		T3	T3		T3		Auditoría de Acceso a Datos
F1	sprint 1		F1	F1		F1	F1		F1		Publicación de Vacantes
T4	sprint 1		T4	T4		T4	T4		T4		Encriptación de Campos Sensibles
F5	sprint 2		F5	F5		F5	F5		F5		Registro de Actividad
I1	sprint 2		I1	I1		I1	I1		I1		Conector e-Sign
I3	sprint 2		I3	I3		I3	I3		I3		Conector HRIS
T1	sprint 2		T1	T1		T1	T1		T1		Centralización de Logs
T2	sprint 2		T2	T2		T2	T2		T2		Monitoreo de Salud
T5	sprint 2		T5	T5		T5	T5		T5		Orquestación de Eventos Fallidos
F3	sprint 2		F3	F3		F3	F3		F3		Evaluación Colaborativa
I2	sprint 2		I2	I2		I2	I2		I2		Integración Outlook/Teams
F4	sprint 3		F4	F4		F4	F4		F4		Notificaciones de Progreso
F6	sprint 3		F6	F6		F6	F6		F6		Seguimiento de Ofertas
T7	sprint 3		T7	T7		T7	T7		T7		Métricas de Performance
F7	sprint 3		F7	F7		F7	F7		F7		Panel de Candidatos
F9	sprint 3		F10	F10		F10	F10		F10		Acceso Seguro (SSO)
T6	sprint 4		T6	T6		T6	T6		T6		Feature Flag de Anonimización

# TICKETS

Historias de Usuario F1 – Publicación de Vacantes

## F1-BE - Backend - Publicación de Vacantes
**Descripción técnica:** Desarrollar el componente backend de 'Publicación de Vacantes', implementando los endpoints necesarios, lógica de negocio, validaciones y control de errores. Asegurar consistencia de datos y manejo eficiente de recursos.

**Criterios de aceptación:** La funcionalidad 'Publicación de Vacantes' opera según especificaciones, sin errores críticos. Los resultados son coherentes con las entradas del usuario o sistema, y se validan los flujos de éxito y error. La implementación cumple estándares internos de calidad y seguridad.

**Story Points:** 8  
**Responsable:** Backend  
**Etiquetas:** Backend, API  
**Repositorio / Módulo:** API  
---

## F1-FE - Frontend - Publicación de Vacantes
**Descripción técnica:** Implementar la interfaz de usuario para 'Publicación de Vacantes', aplicando componentes responsivos, validaciones visuales y mensajes de retroalimentación. Conectar correctamente con los endpoints backend.

**Criterios de aceptación:** La funcionalidad 'Publicación de Vacantes' opera según especificaciones, sin errores críticos. Los resultados son coherentes con las entradas del usuario o sistema, y se validan los flujos de éxito y error. La implementación cumple estándares internos de calidad y seguridad.

**Story Points:** 5  
**Responsable:** Frontend  
**Etiquetas:** Frontend, UI  
**Repositorio / Módulo:** WebApp  
---

## F1-QA - QA - Publicación de Vacantes
**Descripción técnica:** Construir y ejecutar pruebas unitarias, funcionales e integradas que validen el correcto comportamiento de 'Publicación de Vacantes'. Incluir casos de prueba positivos, negativos y de rendimiento.

**Criterios de aceptación:** La funcionalidad 'Publicación de Vacantes' opera según especificaciones, sin errores críticos. Los resultados son coherentes con las entradas del usuario o sistema, y se validan los flujos de éxito y error. La implementación cumple estándares internos de calidad y seguridad.

**Story Points:** 3  
**Responsable:** QA  
**Etiquetas:** Testing  
**Repositorio / Módulo:** QA Suite  
---

## F1-SEC - DevOps - Publicación de Vacantes
**Descripción técnica:** Configurar los servicios, logs y políticas de seguridad e infraestructura asociados a 'Publicación de Vacantes'. Establecer monitoreo, alertas y procedimientos de recuperación ante fallos.

**Criterios de aceptación:** La funcionalidad 'Publicación de Vacantes' opera según especificaciones, sin errores críticos. Los resultados son coherentes con las entradas del usuario o sistema, y se validan los flujos de éxito y error. La implementación cumple estándares internos de calidad y seguridad.

**Story Points:** 5  
**Responsable:** DevOps  
**Etiquetas:** Infraestructura, DevOps  
**Repositorio / Módulo:** Infraestructura  
---

## F1-DOC - Analista Funcional - Publicación de Vacantes
**Descripción técnica:** Redactar la documentación técnica y funcional de 'Publicación de Vacantes', incluyendo diagramas, flujos de datos y referencias a APIs o configuraciones. Garantizar claridad y formato estándar.

**Criterios de aceptación:** La funcionalidad 'Publicación de Vacantes' opera según especificaciones, sin errores críticos. Los resultados son coherentes con las entradas del usuario o sistema, y se validan los flujos de éxito y error. La implementación cumple estándares internos de calidad y seguridad.

**Story Points:** 2  
**Responsable:** Analista Funcional  
**Etiquetas:** Documentación  
**Repositorio / Módulo:** Docs  
---

# Stories Point - Metodologías de cálculo

Los **Story Points** utilizados en el proyecto **ATS LTI** fueron definidos mediante una **metodología híbrida**, combinando prácticas de **Scrum**, **WSJF (Weighted Shortest Job First)** y **RICE (Reach, Impact, Confidence, Effort)**.  
El objetivo fue establecer un modelo de estimación consistente, adaptable y orientado al valor, más allá del simple cálculo en horas.

---

## 1️⃣ Principio base: esfuerzo relativo y complejidad

Los Story Points representan **unidades abstractas de esfuerzo**, no de tiempo.  
Se utilizó la **escala de Fibonacci extendida** (1, 2, 3, 5, 8, 13, 21) para reflejar el crecimiento no lineal de la complejidad.  
Así, una tarea de 13 puntos implica **mayor incertidumbre y coordinación**, no necesariamente el doble de trabajo que una de 8.

---

## 2️⃣ Factores evaluados en cada estimación

Cada historia fue valorada considerando cuatro dimensiones principales:

| Factor | Descripción | Peso estimado |
|--------|--------------|---------------|
| **Complejidad técnica** | Dificultad del desarrollo, arquitectura o infraestructura involucrada. | 40% |
| **Volumen de trabajo** | Cantidad de código, pantallas, endpoints o configuraciones requeridas. | 30% |
| **Riesgo / incertidumbre** | Grado de novedad o dependencia externa. | 20% |
| **Validación y pruebas** | Esfuerzo adicional en QA, documentación o pruebas cruzadas. | 10% |

---

## 3️⃣ Ajustes por tipo de historia

| Tipo | Rango típico | Criterio dominante |
|------|---------------|--------------------|
| **Funcionales (F\*)** | 3–13 | Lógica de negocio, UI/UX, validaciones. |
| **Técnicas (T\*)** | 5–13 | Seguridad, monitoreo, logs, rendimiento. |
| **Integraciones (I\*)** | 3–8 | APIs externas, autenticación, sincronización. |

Cada tipo recibió una calibración base adaptada a su naturaleza: las historias de seguridad y orquestación tienden a mayores puntos por riesgo y criticidad.

---

## 4️⃣ Validación colaborativa

Las estimaciones se simularon mediante una dinámica tipo **Planning Poker**, representando a los roles **Backend, Frontend, QA y DevOps**.  
Se tomaron los promedios ponderados entre equipos, ajustando divergencias mayores al 20%.

---

## 5️⃣ Interpretación práctica

Los Story Points permiten:
- Medir **velocidad del equipo** sin depender de horas.  
- Priorizar con base en **valor entregado vs. esfuerzo requerido**.  
- Integrar métricas WSJF y RICE para decisiones estratégicas de backlog.  

En síntesis, el modelo usado busca **previsibilidad, consistencia y alineación con el valor del producto**, no una equivalencia temporal.

# PROMPTS ARMADOS DE USER STORIES

## PROMPT #1.1

volvemos al proyecto del ATS para la empresa LTI.... te adjunto el archivo con toda la documentación final que desarrollamos (como simple recordatorio ordenador, ya sé que lo posees), porque a partir de esto debemos generar las historias de usuarios para el desarrollo del proyecto. pero antes de que elabores algo, me gustaría que me presentes distintas consideraciones que podría tener en cuenta precisamente para solicitarte esta tarea, así veo cómo encaro la solicitud. 

## PROMPT #1.2

Quiero que me desarrolles al menos 20 historias de usuario, a nivel micro, con el formato clásico (rol, acción, beneficio), agrupados por rol de usuario, que cubran auditoría, logs, monitoreo , seguridad y privacidad, que serán usadas para desarrollo y para backlog. este punto lo profundizaremos en una segunda instancia, con hagas nada todavía al respecto. y acepto tu propuesta de definir una plantilla standard, en función a si serán funcionales, técnicas o de integración.

## PROMPT #1.3

quiero que me generes 10 funcionales, 7 técnicas y 3 de integración. los modelos que me presentaste están perfectos para mí

# PROMPTS ARMADOS DE BACKLOG

## PRIMERA VERSION

### PROMPT #4.1.1

ahora debo armar el Backlog de producto con las User Stories, priorizándolas según algún criterio que considere conveniente. antes de realizar esta tarea, me gustaría que me orientes y me ayudes a recopilar los diferentes criterios que podría tener en cuenta para adoptar una metodología concreta.

### PROMPT #4.1.2

voy a seguir tu consejo, apoyado en los criterios que mencionas sobre el proyecto ATS, y adoptaremos el enfoque híbrido RICE + WSJF. Acepto tu propuesta de hacer una matriz primero con las ponderaciones sugeridas,y sobre ella analizaré la conformación del backlog

#### Criterios complementarios sugeridos para el ATS por el CHATGPT

Dado que el proyecto apunta a multinacionales de RRHH, conviene combinar criterios:
🧩Cumplimiento legal y privacidad: prioridad máxima (requerido por ley).
🧩Valor operativo inmediato: automatización y reducción de tareas repetitivas.
🧩Impacto en la experiencia del reclutador y manager.
🧩Riesgo técnico / de integración: priorizar lo que valida la arquitectura.
🧩Facilidad de testeo / demostración para PoC.

## PROMPT 4.2 - APLICANDO METODOOGIA RICE

### PROMPT 4.2.1

veamos qué backlog resulta utilizando la metodología RICE (alcance, impacto, confianza y esfuerzo)

## PROMPT 4.3 - APLICANDO METODO WSJF

### PROMPT 4.3.1

Armemos el backlog con el criterio WSJF (valor de negocio, urgencia, reducción de riesgo, esfuerzo o complejidad)

## PROMPT 4.4 - APLICANDO METODO MoSCoW

### PROMPT 4.4.1

generamos un backlog aplicando el método MoSCoW (Must Have, Should Have, Could Have, Won't Have)

## PROMPT 4.5 - APLICANDO METODO KANO MODEL

### PROMPT 4.5.1

generamos un backlog aplicando la metodología Kano Model (necesidades básicas, necesidades de rendimiento, sorpresas)

