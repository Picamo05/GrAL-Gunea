# Guía de Bootstrap 5 para este proyecto

> **Instrucciones para la IA:** este proyecto usa **Bootstrap v5.3.x** vía CDN. Sigue esta guía en todo el HTML/CSS que generes. Usa clases de Bootstrap antes que CSS propio, diseña con enfoque **Mobile-First** y no uses jQuery.

## 1. Principios

- **Mobile-First:** se diseña primero para móvil y después se adapta a pantallas grandes con prefijos de breakpoint (`sm`, `md`, `lg`, `xl`, `xxl`). Una interfaz, varios diseños.
- **Sin jQuery:** Bootstrap 5 usa JavaScript nativo. No añadir jQuery.
- **Variables CSS nativas:** permiten personalizar rápido y soportan modo claro/oscuro.
- **Prioridad:** clases de Bootstrap → utilidades → CSS propio solo si es imprescindible.

## 2. Integración por CDN (Quick Start)

No hay que descargar nada. Plantilla base:

```html
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
          rel="stylesheet"
          integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB"
          crossorigin="anonymous">
  </head>
  <body>
    <h1>Hello, world!</h1>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"
            integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI"
            crossorigin="anonymous"></script>
  </body>
</html>
```

Checklist obligatorio:

- [ ] Meta etiqueta **viewport** en el `<head>` (imprescindible para responsive).
- [ ] Enlace al **CSS** de Bootstrap en el `<head>`.
- [ ] **JS Bundle** al final del `<body>` (incluye Popper).

Documentación: https://getbootstrap.com/docs/5.3/getting-started/introduction/#quick-start

## 3. Breakpoints

| Breakpoint | Prefijo | Ancho mínimo |
|---|---|---|
| Extra Small | `.col-` | < 576px (móviles) |
| Small | `.col-sm-` | ≥ 576px (móviles anchos) |
| Medium | `.col-md-` | ≥ 768px (tablets) |
| Large | `.col-lg-` | ≥ 992px (escritorio) |
| Extra Large | `.col-xl-` | ≥ 1200px (pantallas grandes) |
| XXL | `.col-xxl-` | ≥ 1400px (pantallas muy grandes) |

Los prefijos se aplican **desde ese ancho hacia arriba**. Sin prefijo = todos los tamaños.

## 4. Sistema Grid

- Cada `.row` se divide en **12 columnas**.
- La suma de columnas de una fila debe ser **12**; si se supera, las columnas sobrantes pasan automáticamente a la siguiente línea.
- Estructura: `.container` (o `.container-fluid`) → `.row` → `.col-*`.
- Combinar tamaños para cada breakpoint, por ejemplo `col-12 col-sm-6 col-xl-3`:
  - móvil: 1 por fila,
  - ≥ 576px: 2 por fila,
  - ≥ 1200px: 4 por fila.
- **Habiatzea (anidado):** dentro de una `.col-*` se puede poner otra `.row` con `.col-*` más pequeñas.

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-6">
      <div class="row">
        <div class="col-4">Icono</div>
        <div class="col-8">Valor</div>
      </div>
    </div>
    <div class="col-12 col-md-6">...</div>
  </div>
</div>
```

## 5. Utilidades de visibilidad (Display)

| Clase | Efecto |
|---|---|
| `.d-none` | Oculta el elemento en todas las pantallas |
| `.d-md-block` | Lo muestra como bloque desde pantallas medianas |
| `.d-lg-flex` | Lo convierte en contenedor Flexbox desde pantallas grandes |

Patrón habitual para **ocultar en móvil y mostrar en escritorio**: `d-none d-lg-block`.
Úsalo para reducir la carga cognitiva en pantallas pequeñas (gráficos o detalles pesados).

## 6. Flexbox

| Función | Clases |
|---|---|
| Activar flex | `d-flex` |
| Justificación (eje principal) | `justify-content-start` / `center` / `end` / `between` / `around` |
| Alineación vertical (eje cruzado) | `align-items-start` / `center` / `end` |
| Dirección | `flex-row` / `flex-column` |
| Alineación de texto responsive | `text-start`, `text-center`, `text-end`, `text-sm-end`, `text-md-end`, `text-lg-end`, `text-xl-end`, `text-xxl-end` |

Patrón típico de cabecera de tarjeta: `d-flex justify-content-between align-items-center`.

Ejemplos de referencia: https://getbootstrap.com/docs/5.3/examples/grid/

---

## 7. Ejercicio 1: Página de producto "Music Store"

**Tareas**

1. Crear un `<header>` principal usando `.container`.
2. Imagen de la portada del disco: `col-12 col-md-5`.
3. Datos del álbum: `col-12 col-md-7`.

**Objetivo UX:** en móvil, imagen arriba y texto debajo (apilados); en pantallas grandes, dos columnas.

> **Nota sobre el orden:** el enunciado original pide la imagen a la derecha y los datos a la izquierda en escritorio, pero imagen arriba en móvil. Para cumplir ambas cosas, pon la imagen primero en el HTML (así queda arriba en móvil) y reordénala en escritorio con `order-md-*`:

```html
<header class="container my-4">
  <div class="row align-items-center">
    <div class="col-12 col-md-5 order-md-2">
      <img src="https://placehold.co/600x400" class="img-fluid rounded" alt="Portada del disco">
    </div>
    <div class="col-12 col-md-7 order-md-1">
      <h1>Título del álbum</h1>
      <p>Artista, año, géneros, lista de canciones, precio...</p>
    </div>
  </div>
</header>
```

## 8. Ejercicio 2: Dashboard de métricas

**Enunciado:** desarrollar la interfaz de un panel de gestión (Metrics Dashboard) con KPIs, que se adapte automáticamente de móvil a escritorio.

**Comportamiento esperado**

- **Escritorio:** tarjetas y paneles en paralelo.
- **Tablet:** matriz de 2 columnas.
- **Móvil:** una sola columna, minimizando la carga cognitiva.

**Guion de trabajo**

1. **Estructura general**
   - Documento HTML con el CDN de Bootstrap 5.
   - `.container-fluid` como contenedor de todo el panel, con una barra de navegación (`navbar`) principal arriba.
2. **Tarjetas de métricas (Grid)**
   - Una fila `.row` de 3 o 4 columnas en la parte superior con datos de ventas.
   - Clases combinadas: `col-12 col-sm-6 col-xl-3` (móvil: una tarjeta por fila; pantallas grandes: cuatro por fila).
3. **Contenido anidado y Flexbox**
   - Dentro de cada tarjeta, estructuras anidadas (`.row` y `.col-*` más pequeñas) para repartir iconos y valores numéricos.
   - Flexbox en la cabecera de la tarjeta: `d-flex justify-content-between align-items-center`.
4. **Control de visibilidad**
   - Añadir `d-none d-lg-block` a algunos detalles o gráficos secundarios, para ocultar información pesada en smartphone y mostrarla solo en dispositivos grandes.
5. **Prueba y validación**
   - Comprobar con las herramientas de desarrollador del navegador cómo responde el diseño en cada breakpoint.

**Esqueleto de ejemplo**

```html
<nav class="navbar navbar-dark bg-dark">
  <div class="container-fluid">
    <span class="navbar-brand">Metrics Dashboard</span>
  </div>
</nav>

<main class="container-fluid py-4">
  <div class="row g-3">
    <div class="col-12 col-sm-6 col-xl-3">
      <div class="card h-100">
        <div class="card-body">
          <div class="d-flex justify-content-between align-items-center">
            <div class="row w-100 align-items-center">
              <div class="col-4 fs-1">📈</div>
              <div class="col-8 text-end">
                <h5 class="card-title mb-0">Ventas</h5>
                <p class="fs-3 mb-0">12.450 €</p>
              </div>
            </div>
          </div>
          <div class="d-none d-lg-block mt-3">
            <small class="text-muted">Detalle extra solo visible en pantallas grandes</small>
          </div>
        </div>
      </div>
    </div>
    <!-- Repetir para las demás tarjetas -->
  </div>
</main>
```

---

## 9. Reglas para la IA al generar código

1. Incluir siempre la plantilla base (viewport + CSS + JS bundle) en los documentos nuevos.
2. Usar `.container` o `.container-fluid` > `.row` > `.col-*`, sin saltarse niveles.
3. Declarar siempre `col-12` (o la columna base) para el caso móvil y añadir prefijos para tamaños mayores.
4. No pasar de 12 columnas por fila salvo que se quiera forzar el salto de línea.
5. Preferir utilidades de Bootstrap (`d-*`, `flex-*`, `justify-*`, `align-*`, `text-*`, `g-*`, `my-*`, `p-*`) al CSS personalizado.
6. Añadir `alt` a las imágenes y `img-fluid` para que sean responsive.
7. No usar jQuery.
8. Documentación de referencia: https://getbootstrap.com/docs/5.3/
