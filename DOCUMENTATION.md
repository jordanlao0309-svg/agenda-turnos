# Documentación Técnica - Agenda de Turnos

## 1. Descripción General
"Agenda de Turnos" es una aplicación web de una sola página (SPA) diseñada para gestionar los horarios de trabajo del personal. Permite a los usuarios registrar nuevos turnos, visualizarlos en una lista y eliminarlos cuando ya no sean necesarios. El objetivo principal es ofrecer una interfaz rápida, intuitiva y persistente sin requerir configuración de servidores o bases de datos externas.

## 2. Tecnologías Utilizadas
El proyecto está construido utilizando tecnologías web estándar (Vanilla Web Stack):
- **HTML5:** Estructura semántica de la aplicación.
- **CSS3:** Estilos, diseño responsive básico y animaciones visuales (uso de Flexbox y degradados).
- **JavaScript (ES6):** Lógica de negocio y manipulación del DOM.
- **LocalStorage API:** Para la persistencia de datos en el navegador del usuario.

## 3. Estructura del Proyecto
Toda la lógica, estilos y estructura se encuentran encapsulados principalmente en el archivo `index.html` para mantener la simplicidad:
- **Cabecera (`<head>`):** Importación de la fuente de Google Fonts ("Inter") y declaración de estilos CSS internos (`<style>`).
- **Cuerpo (`<body>`):** 
  - Contenedor izquierdo (`.left`): Muestra el título y la descripción de la herramienta.
  - Contenedor derecho (`.right`): Contiene el formulario de entrada y la lista de turnos renderizados dinámicamente.
- **Scripts (`<script>`):** Lógica de estado y eventos.

*Nota: Existe un archivo `style.css` en el directorio, pero los estilos principales que utiliza el proyecto en su versión actual se encuentran incrustados en `index.html`.*

## 4. Almacenamiento de Datos (Persistencia)
El sistema utiliza el `localStorage` del navegador para guardar los datos. Esto significa que la información no se pierde al recargar o cerrar la pestaña.
- **Clave de almacenamiento:** `"turnos"`
- **Formato:** Los datos se guardan como un arreglo (Array) de objetos serializado en formato JSON.
- **Estructura de un Turno:**
  ```json
  {
    "nombre": "Juan Pérez",
    "turno": "mañana",
    "inicio": "08:00",
    "fin": "16:00",
    "fecha": "2026-06-15"
  }
  ```

## 5. Funciones de JavaScript Principales

El flujo de la aplicación se maneja mediante 4 funciones clave:

- `guardar()`: Convierte el arreglo global de `turnos` a una cadena JSON y lo guarda en el `localStorage`.
- `agregar()`: Obtiene los valores de los inputs (nombre, turno, inicio, fin, fecha). Valida que todos los campos estén completos. Si es exitoso, crea un objeto, lo inserta en el arreglo `turnos`, llama a `guardar()` y actualiza la vista con `mostrar()`.
- `eliminar(i)`: Recibe el índice (`i`) del turno a eliminar. Utiliza el método `splice()` para quitar el elemento del arreglo, luego llama a `guardar()` y actualiza la vista con `mostrar()`.
- `mostrar()`: Limpia el contenedor de la lista de turnos en el DOM y vuelve a renderizar todos los elementos iterando sobre el arreglo `turnos`. Genera dinámicamente elementos HTML y asigna clases de colores dependiendo del tipo de turno (mañana, tarde, noche).

## 6. Diseño y Estilos
El diseño de la aplicación destaca por un esquema de colores vibrantes y una estructura limpia:
- **Background:** Degradado moderno lineal (`linear-gradient(135deg, #4facfe, #00f2fe)`).
- **Tipografía:** "Inter" sans-serif.
- **Contenedores:** Se utiliza Flexbox (`display: flex`) para alinear tanto el contenedor principal (dividiendo la pantalla en dos columnas 40/60) como los elementos individuales de los turnos.
- **Feedback visual:** Botones con efectos de `hover` y etiquetas (badges) de diferentes colores para clasificar visualmente el tipo de turno:
  - Mañana: Verde (`#22c55e`)
  - Tarde: Naranja (`#f59e0b`)
  - Noche: Índigo (`#6366f1`)
