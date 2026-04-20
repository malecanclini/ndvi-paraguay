# 🗺️ NDVI Paraguay — Mapa Interactivo

Visualizador web interactivo del **Índice de Vegetación por Diferencia Normalizada (NDVI)** para los 17 departamentos y la capital de Paraguay. Construido con HTML, CSS y JavaScript puro usando **Leaflet.js**.

![Paraguay NDVI Map](https://img.shields.io/badge/Leaflet-1.9.4-199900?style=flat-square&logo=leaflet)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![HTML](https://img.shields.io/badge/HTML-standalone-orange?style=flat-square)

---

## 📸 Vista previa

> Mapa oscuro interactivo con capas NDVI por temporada, panel de estadísticas y selección por departamento.

---

## 🌿 ¿Qué es el NDVI?

El **NDVI** (Normalized Difference Vegetation Index) es un índice espectral que mide la densidad y salud de la vegetación a partir de imágenes satelitales. Se calcula como:

```
NDVI = (NIR - RED) / (NIR + RED)
```

| Rango | Interpretación |
|-------|---------------|
| 0.7 – 0.9 | Vegetación muy densa (bosques, selvas) |
| 0.5 – 0.7 | Vegetación alta (cultivos, pasturas) |
| 0.3 – 0.5 | Vegetación media |
| 0.1 – 0.3 | Vegetación escasa o degradada |
| < 0.1 | Suelo desnudo, zonas urbanas, agua |

---

## ✨ Características

- 🗺️ **Mapa interactivo** con Leaflet.js y fondo CartoDB Dark Matter
- 🌱 **18 polígonos departamentales** coloreados según valor NDVI
- 📅 **4 temporadas** — Verano, Otoño, Invierno, Primavera — con actualización en tiempo real
- 🖱️ **Tooltip** al pasar el cursor con nombre y valor NDVI
- 📊 **Panel lateral** con escala de colores, detalles del departamento seleccionado y estadísticas nacionales
- 🌙 **Tema oscuro** completo, sin dependencias de frameworks CSS
- 📁 **Archivo único** autocontenido — sin build tools, sin Node.js, sin bundlers

---

## 🚀 Uso

### Opción 1 — Abrir directamente

Descarga `ndvi-paraguay.html` y ábrelo en cualquier navegador moderno:

```bash
# Clonar el repositorio
git clone https://github.com/tu-usuario/ndvi-paraguay.git
cd ndvi-paraguay

# Abrir en el navegador
open ndvi-paraguay.html         # macOS
start ndvi-paraguay.html        # Windows
xdg-open ndvi-paraguay.html     # Linux
```

### Opción 2 — Servidor local (recomendado)

```bash
# Con Python
python -m http.server 8080

# Con Node.js
npx serve .
```

Luego ir a `http://localhost:8080/ndvi-paraguay.html`

### Opción 3 — GitHub Pages

1. Ir a **Settings → Pages** en tu repositorio
2. Source: `Deploy from a branch` → rama `main`, carpeta `/ (root)`
3. El mapa quedará disponible en `https://tu-usuario.github.io/ndvi-paraguay/ndvi-paraguay.html`

---

## 📂 Estructura del proyecto

```
ndvi-paraguay/
├── ndvi-paraguay.html   # Aplicación completa (único archivo)
└── README.md            # Este archivo
```

---

## 🔧 Tecnologías

| Tecnología | Versión | Uso |
|-----------|---------|-----|
| [Leaflet.js](https://leafletjs.com/) | 1.9.4 | Motor de mapas interactivos |
| [CartoDB Basemaps](https://carto.com/basemaps/) | — | Mapa base oscuro |
| [IBM Plex Sans / Mono](https://fonts.google.com/specimen/IBM+Plex+Sans) | — | Tipografía |
| HTML / CSS / JS | ES6+ | Sin frameworks |

---

## 📡 Datos NDVI

> ⚠️ Los valores NDVI incluidos en esta versión son **estimaciones representativas** basadas en patrones climáticos y estacionales conocidos de Paraguay. No provienen de imágenes satelitales reales.

### Fuentes de datos reales recomendadas

Para integrar datos satelitales reales, se pueden usar las siguientes fuentes:

| Fuente | Producto | Resolución | Acceso |
|--------|---------|-----------|--------|
| NASA / USGS | MODIS MOD13A3 | 1 km / mensual | [earthdata.nasa.gov](https://earthdata.nasa.gov) |
| ESA | Sentinel-2 MSI | 10 m / 5 días | [scihub.copernicus.eu](https://scihub.copernicus.eu) |
| Google Earth Engine | MOD13A3, S2 | Variable | [earthengine.google.com](https://earthengine.google.com) |
| INPE (Brasil) | TerraClass | 30 m / anual | [inpe.br](http://www.inpe.br) |

### Ejemplo — Google Earth Engine (JavaScript)

```javascript
var py = ee.FeatureCollection("FAO/GAUL/2015/level1")
  .filter(ee.Filter.eq('ADM0_NAME', 'Paraguay'));

var modis = ee.ImageCollection("MODIS/006/MOD13A3")
  .filterDate('2023-01-01', '2023-12-31')
  .select('1_km_monthly_NDVI')
  .mean()
  .clip(py);

Map.addLayer(modis, {min: 0, max: 9000, palette: ['d4a017','cddc39','8bc34a','4caf50','1a6b1a']}, 'NDVI 2023');
```

---

## 🗺️ Departamentos incluidos

| Región | Departamentos |
|--------|-------------|
| **Chaco** | Alto Paraguay, Boquerón, Presidente Hayes |
| **Oriental** | Concepción, San Pedro, Cordillera, Guairá, Caaguazú, Caazapá, Itapúa, Misiones, Paraguarí, Alto Paraná, Central, Ñeembucú, Amambay, Canindeyú |
| **Capital** | Asunción |

---

## 🛠️ Personalización

### Cambiar los valores NDVI

Editar el objeto `NDVI_DATA` en el archivo HTML:

```javascript
const NDVI_DATA = {
  summer: {
    "Itapúa": 0.74,   // ← reemplazar con datos reales
    "Canindeyú": 0.78,
    // ...
  }
};
```

### Agregar una nueva temporada

```javascript
const NDVI_DATA = {
  // ... temporadas existentes ...
  custom: {
    "Alto Paraguay": 0.55,
    // ... todos los departamentos ...
  }
};
```

Y agregar el botón correspondiente en el HTML:

```html
<button class="season-btn" data-season="custom">Mi período</button>
```

---

## 📄 Licencia

MIT © 2024 — libre para uso personal, académico y comercial.

---

## 🙌 Contribuciones

Las contribuciones son bienvenidas. Para cambios importantes, abrir un issue primero para discutir qué te gustaría cambiar.

1. Fork del repositorio
2. Crear rama: `git checkout -b feature/mejora-ndvi`
3. Commit: `git commit -m 'Agrega datos MODIS reales'`
4. Push: `git push origin feature/mejora-ndvi`
5. Abrir Pull Request

---

*Desarrollado con datos de vegetación de Paraguay 🌿*
