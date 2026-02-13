# Historia de Usuario

## ID
HU-XXX

## Título
Dashboard de Monitoreo Climático en Tiempo Real

## Descripción
**Como** Viticultor de las D.O. de Txakoli (Getaria, Bizkaia o Araba)

**Quiero** visualizar los datos actuales de temperatura, humedad y precipitaciones de mi ubicación.

**Para** identificar si las condiciones ambientales actuales suponen un riesgo de enfermedades como el Mildiú o la Botrytis.

## Criterios de Aceptación

### Escenario 1: Carga exitosa de datos meteorológicos
```gherkin
Dado que el usuario accede a la vista principal (Dashboard).

Cuando la aplicación se conecta exitosamente con la API de Open-Meteo.

Entonces se deben visualizar los valores actuales de Temperatura (°C), Humedad (%) y Precipitaciones (mm) Y el sistema debe dejar de mostrar el estado de carga inicial gestionado por <Suspense />.
```

### Escenario 2: Notificación de condiciones de riesgo
```gherkin
Dado que recibidos de la API datos metereologicos como temperatura y humedad del suelo, temperatura y humedad ambiental, evapotranspiración, precipitación, covertura de nubes y horas de sol, heladas tempranas.

Cuando el sistema procesa los parámetros.

Entonces se debe mostrar una alerta visual indicando "Riesgo de Enfermedad detectado", y/o "Riesgo por Condiciones Meteorológicas Adversas" y en su caso dar una recomendación.
```

## Notas
**API Fuente:** Se utilizará https://open-meteo.com/en/docs.

**Reactividad:** Es obligatorio el uso de ref y reactive para la actualización automática de los datos.

**Estilo:** Se debe aplicar la metodología BEM para el diseño de las tarjetas de datos.

## Estimación
M (Talla Media)

## Prioridad
Alta (Funcionalidad Core)

## Tareas
| Código | Nombre | Responsable |
| :--- | :--- | :--- |
| **HU-001-01** | Configuración de la conexión asíncrona a la API Open-Meteo en `services/` | Equipo Dev |
| **HU-001-02** | Creación del Composable `useWeather.ts` para gestionar la lógica de fetching | Equipo Dev |
| **HU-001-03** | Diseño de componentes atómicos (`DataCard`) siguiendo Atomic Design | Equipo Dev |
| **HU-001-04** | Implementación de la vista `DashboardView.vue` con soporte para `<Suspense />` | Equipo Dev |


# Historia de Usuario

## ID
HU-XXX

## Título
[Título descriptivo de la historia]

## Descripción
**Como** [tipo de usuario]
**Quiero** [acción o funcionalidad]
**Para** [beneficio o valor]

## Criterios de Aceptación

### Escenario 1: [Nombre del escenario]
```gherkin
Dado [contexto inicial]
Cuando [acción del usuario]
Entonces [resultado esperado]
```

### Escenario 2: [Nombre del escenario]
```gherkin
Dado [contexto inicial]
Cuando [acción del usuario]
Entonces [resultado esperado]
```

## Notas
[Información adicional, dependencias, restricciones...]

## Estimación
[Puntos de historia / Talla (S, M, L, XL)]

## Prioridad
[Alta / Media / Baja]

## Tareas
| Código | Nombre | Responsable |
|--------|--------|-------------|
| HU-XXX-01 | [Descripción de la tarea] | [Nombre] |
| HU-XXX-02 | [Descripción de la tarea] | [Nombre] |



# Historia de Usuario

## ID
HU-002

## Título
Gestión de Parcelas y Alertas Personalizadas (CRUD)

## Descripción
**Como** Viticultor de Txakoli 

**Quiero** Registrar, editar y eliminar los datos de mis parcelas (nombre, ubicación y D.O.).

**Para**  Tener un control organizado de mis cultivos y recibir alertas específicas según la zona de cada viñedo.

## Criterios de Aceptación

### Escenario 1: Registro de una nueva parcela
```gherkin
Dado que el viticultor se encuentra en la sección "My Vineyards"

Cuando completa el formulario con el nombre de la parcela y selecciona su D.O. (Getaria, Bizkaia o Araba)

Entonces el sistema debe guardar los datos en el servidor local (Json-Server) mediante una petición POST Y la nueva parcela debe aparecer inmediatamente en la lista de cultivos.
```

### Escenario 2: Eliminación de una parcela existente
```gherkin
Dado que el viticultor tiene parcelas registradas en su panel.

Cuando pulsa el botón "Delete" en una de las parcelas.

Entonces el sistema debe realizar una petición DELETE al servidor y el elemento debe desaparecer de la interfaz sin necesidad de recargar la página.
```

## Notas
**Backend:** Se requiere tener activo el json-server --watch db.json.

**Tecnología:** Uso de v-for para iterar sobre la lista de parcelas y v-model para el formulario.

**Validación:** No se deben permitir nombres de parcelas vacíos.

## Estimación
L (Talla Grande - requiere configuración de CRUD completo).

## Prioridad
Alta (Requisito obligatorio de gestión de datos propios).

## Tareas
| Código | Nombre | Responsable |
| :--- | :--- | :--- |
| **HU-002-01** | Configuración del archivo `db.json` con la estructura inicial de parcelas | Equipo Dev |
| **HU-002-02** | Implementación del servicio de API para CRUD (Get, Post, Put, Delete) | Equipo Dev |
| **HU-002-03** | Creación del componente de formulario `AddParcelForm.vue` (Molecule) | Equipo Dev |
| **HU-002-04** | Desarrollo de la vista `VineyardsView.vue` para listar y gestionar ítems | Equipo Dev |
