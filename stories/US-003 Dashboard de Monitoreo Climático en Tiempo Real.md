# Historia de Usuario

## ID
US-003

## Título
Dashboard de Monitoreo Climático en Tiempo Real

## Descripción
**Como** Viticultor de las D.O. de Txakoli
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
| **TK-003-01** | Configuración de la conexión asíncrona a la API Open-Meteo en `services/` | Equipo Dev |
| **TK-003-02** | Creación del Composable `useWeather.ts` para gestionar la lógica de fetching | Equipo Dev |
| **TK-003-03** | Diseño de componentes atómicos (`DataCard`) siguiendo Atomic Design | Equipo Dev |
| **TK-003-04** | Implementación de la vista `DashboardView.vue` con soporte para `<Suspense />` | Equipo Dev |