# Historia de Usuario

## ID
HU-001

## Título

Acceso Seguro al Sistema (Login) y Registro de Usuario

## Descripción
**Como** Viticultor interesado en proteger mi cultivo de Hondarrabi Zuri

**Quiero** poder registrarme y autenticarme en la plataforma

**Para** acceder de manera privada a las métricas de mis parcelas y recibir alertas personalizadas

## Criterios de Aceptación

### Escenario 1: Registro de nuevo usuario
```gherkin
Dado que el viticultor no tiene una cuenta
Cuando introduce su email y una contraseña segura en el formulario de registro
Entonces sus datos se almacenan en el sistema (Json-Server) 
Y se le redirige automáticamente a la pantalla de Login.
```

### Escenario 2: Inicio de sesión exitoso
```gherkin
Dado que el usuario ya está registrado
Cuando introduce sus credenciales correctas
Entonces el sistema valida los datos contra el servidor 
Y lo redirige al Dashboard principal de VitisGuard.
```

### Escenario 3: Inicio de sesión exitoso
```gherkin
Dado que el usuario intenta registrarse o loguearse
Cuando deja campos vacíos o introduce un formato de email incorrecto
Entonces el sistema muestra mensajes de error en inglés (ej: "Email is required")
```

## Notas
* Se utilizará Pinia para gestionar el estado global de la sesión del usuario (`isLoggedIn`, `userData`)

* Las contraseñas en el servidor fake (`db.json`) deben manejarse siguiendo las buenas prácticas de seguridad mencionadas en el proyecto.

## Estimación

M (Talla Media)

## Prioridad

Alta (Bloqueante para el resto de funcionalidades)

## Tareas
| Código | Nombre | Responsable |
|--------|--------|-------------|
| HU-001-01 | Diseño de la interfaz de Login/Registro en Figma (Responsive) | Equipo Dev |
| HU-001-02 | Implementación del formulario con validaciones en Vue 3 | Equipo Dev |
| HU-001-03 | Creación del Store de autenticación con Pinia | Equipo Dev |
| HU-001-04 | Servicio de conexión con Json-Server para persistencia de usuarios | Equipo Dev |

## ID
HU-002

## Título
Dashboard Integral de Monitoreo y Alerta Temprana

## Descripción
**Como** Viticultor de Txakoli

**Quiero** visualizar un panel con datos de temperatura, humedad (suelo/aire), evapotranspiración, nubes, heladas y golpes de calor

**Para**  recibir alertas automáticas de riesgo de enfermedades o condiciones adversas y tomar medidas preventivas que protejan mi cosecha.

## Criterios de Aceptación

### Escenario 1: Visualización de métricas críticas
```gherkin
Dado que el usuario ha iniciado sesión

Cuando carga el Dashboard

Entonces debe ver tarjetas con datos en tiempo real de:
  - Temperatura y Humedad Ambiental 
  - Temperatura y Humedad del Suelo 
  - Evapotranspiración 
  - Precipitación y Cobertura de Nubes 
  - Horas de sol y detección de Heladas Fuertes o Golpes de Calor 
Y los datos deben provenir de la API de Open-Meteo
```

### Escenario 2: Activación de Alertas y Recomendaciones por enfermedad
```gherkin
Dado que los datos de la API cumplen condiciones de riesgo por enfermedad fúngica (ej. alta humedad y temperaturas moderadas)

Cuando el componente procesa los datos

Entonces se muestra la alerta: "Riesgo de posible Enfermedad detectado" y se especifican riesgos como Mildiú, Botrytis, Oídio o Excoriosis y se ofrece una recomendación específica (ej. aumentar aireación constante en espalderas)
```

### Escenario 3: Activación de Alertas por condiciones meteorológicas adversas
```gherkin
Dado que los datos de la API detectan riesgos como heladas tempranas, tormentas o calor extremo

Cuando el componente procesa los datos

Entonces se muestra la alerta: "Riesgo por condiciones meteorológicas adversas" y se especifica el fenómeno detectado (ej. Helada inminente o exceso de pluviosidad) y se ofrece una recomendación específica (ej. cubrir lote, activar drenaje preventivo o regar para refrescar)
```

## Notas
* **Lógica de Alerta:** Las alertas por enfermedad deben activarse especialmente en "años con datos historicos muy humedos".

* **Requerimiento Técnico:** Se utilizarán las etiquetas `<suspense/>` para gestionar la espera de datos asíncronos de la API.

* **Responsive:** El Dashboard debe adaptarse a dispositivos móviles, tablets y escritorio.

## Estimación
L (Talla Grande).

## Prioridad
Alta.

## Tareas
| Código | Nombre | Responsable |
| :--- | :--- | :--- |
| **HU-002-01** | Implementación de peticiones a Open-Meteo para métricas de suelo y aire| Equipo Dev |
| **HU-002-02** | Desarrollo de la lógica de negocio para detectar umbrales de Mildiú y Botrytis | Equipo Dev |
| **HU-002-03** | Creación de componentes de alerta con directivas `v-show`/`v-if` | Equipo Dev |
| **HU-002-04** | Sistema de recomendaciones dinámicas basadas en el estado del cultivo | Equipo Dev |


## ID
HU-003

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
| **HU-003-01** | Configuración de la conexión asíncrona a la API Open-Meteo en `services/` | Equipo Dev |
| **HU-003-02** | Creación del Composable `useWeather.ts` para gestionar la lógica de fetching | Equipo Dev |
| **HU-003-03** | Diseño de componentes atómicos (`DataCard`) siguiendo Atomic Design | Equipo Dev |
| **HU-003-04** | Implementación de la vista `DashboardView.vue` con soporte para `<Suspense />` | Equipo Dev |

## ID
HU-004

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
| **HU-004-01** | Configuración del archivo `db.json` con la estructura inicial de parcelas | Equipo Dev |
| **HU-004-02** | Implementación del servicio de API para CRUD (Get, Post, Put, Delete) | Equipo Dev |
| **HU-004-03** | Creación del componente de formulario `AddParcelForm.vue` (Molecule) | Equipo Dev |
| **HU-004-04** | Desarrollo de la vista `VineyardsView.vue` para listar y gestionar ítems | Equipo Dev |

