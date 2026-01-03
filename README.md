# 🗺️ Área Inundable Colonias Río Potinaspak

Mapa interactivo de áreas inundables en las colonias cercanas al Río Potinaspak.

## 📋 Descripción

Este proyecto contiene mapas geoespaciales que muestran las zonas de riesgo de inundación en las colonias cercanas al Río Potinaspak. Los mapas fueron elaborados en QGIS y están disponibles para visualización web interactiva.

## 🌐 Visualización del Mapa

### Opción 1: GitHub Pages (Recomendado)

El mapa se puede visualizar directamente en línea a través de GitHub Pages:

**URL:** https://JAAT120686.github.io/-rea_inundable_colonias_rio_Potinaspak/

Para habilitar GitHub Pages:
1. Ve a la configuración del repositorio (Settings)
2. En la sección "Pages" del menú lateral
3. En "Source" selecciona la rama `main` (o la rama donde está el código)
4. Selecciona la carpeta `/root`
5. Haz clic en "Save"
6. Espera unos minutos y el mapa estará disponible en la URL anterior

### Opción 2: Visualización Local

Para ver el mapa localmente:

```bash
# Clona el repositorio
git clone https://github.com/JAAT120686/-rea_inundable_colonias_rio_Potinaspak.git
cd -rea_inundable_colonias_rio_Potinaspak

# Abre el archivo index.html en tu navegador
# En Linux/Mac:
xdg-open index.html
# O simplemente abre el archivo index.html con tu navegador favorito
```

O usa un servidor web simple:

```bash
# Con Python 3
python -m http.server 8000

# Con Python 2
python -m SimpleHTTPServer 8000

# Con Node.js (si tienes npx)
npx serve

# Luego abre http://localhost:8000 en tu navegador
```

## 📂 Estructura del Proyecto

```
-rea_inundable_colonias_rio_Potinaspak/
├── index.html              # Mapa web interactivo
├── data/                   # Datos geoespaciales en formato GeoJSON
│   ├── areas_inundables.geojson
│   ├── rio.geojson
│   └── colonias.geojson
├── docs/                   # Documentación adicional
│   └── INSTRUCCIONES_QGIS.md
└── README.md              # Este archivo
```

## 🛠️ Cómo Exportar Mapas desde QGIS

### Paso 1: Preparar el Proyecto en QGIS

1. Abre tu proyecto en QGIS
2. Asegúrate de que todas las capas estén en el sistema de coordenadas WGS 84 (EPSG:4326)
3. Organiza tus capas con nombres descriptivos

### Paso 2: Exportar a GeoJSON

Para cada capa que quieras visualizar en el mapa web:

1. Haz clic derecho en la capa → **Exportar** → **Guardar objetos como...**
2. Selecciona el formato: **GeoJSON**
3. Elige el SRC: **EPSG:4326 - WGS 84**
4. Guarda el archivo en la carpeta `data/` con un nombre descriptivo
5. En las opciones, puedes seleccionar:
   - **Precisión de coordenadas:** 6 decimales
   - **Codificación:** UTF-8

### Paso 3: Configurar Propiedades de las Capas

Asegúrate de que tus capas GeoJSON tengan las siguientes propiedades para mejor visualización:

- `nombre`: Nombre de la zona o colonia
- `riesgo`: Nivel de riesgo (alto, medio, bajo)
- `descripcion`: Descripción adicional

Ejemplo de propiedades en QGIS:
```
nombre: Colonia Centro
riesgo: alto
descripcion: Zona con alto riesgo de inundación durante la temporada de lluvias
```

### Paso 4: Actualizar el Mapa Web

Después de exportar tus archivos GeoJSON:

1. Coloca los archivos en la carpeta `data/`
2. Si usaste nombres diferentes, actualiza las rutas en `index.html` (líneas con `loadGeoJSON`)
3. Ajusta las coordenadas del centro del mapa en `index.html` si es necesario
4. Commit y push de los cambios al repositorio

```bash
git add data/*.geojson
git add index.html
git commit -m "Actualizar datos geoespaciales del mapa"
git push origin main
```

## 🎨 Personalización

### Cambiar Colores del Mapa

Edita la función `getStyle` en `index.html` para cambiar los colores según tus preferencias:

```javascript
case 'alto':
    color = 'rgba(255, 0, 0, 0.5)';  // Rojo para alto riesgo
    break;
```

### Cambiar el Centro del Mapa

Modifica las coordenadas en la línea de inicialización del mapa:

```javascript
var map = L.map('map').setView([LATITUD, LONGITUD], ZOOM);
```

### Agregar Más Capas Base

Puedes agregar otros proveedores de mapas base como Google Maps, MapBox, etc. Consulta la [documentación de Leaflet](https://leafletjs.com/reference.html#tilelayer).

## 📊 Datos y Capas

El mapa incluye las siguientes capas de información:

- **Áreas Inundables:** Zonas clasificadas por nivel de riesgo
  - Alto riesgo (rojo)
  - Riesgo medio (naranja)
  - Riesgo bajo (amarillo)
- **Río Potinaspak:** Cauce del río
- **Colonias:** Límites de las colonias afectadas

## 🤝 Contribuciones

Si deseas contribuir con actualizaciones al mapa:

1. Haz fork del repositorio
2. Crea una rama para tus cambios (`git checkout -b mejoras-mapa`)
3. Realiza tus cambios y exporta los datos actualizados
4. Commit tus cambios (`git commit -am 'Actualización de áreas inundables'`)
5. Push a la rama (`git push origin mejoras-mapa`)
6. Crea un Pull Request

## 📝 Licencia

Este proyecto está bajo la licencia especificada en el archivo LICENSE.

## ℹ️ Información Adicional

- **Tecnologías utilizadas:** Leaflet.js, OpenStreetMap, GeoJSON
- **Software de creación:** QGIS
- **Sistema de coordenadas:** WGS 84 (EPSG:4326)

Para más información o preguntas, por favor abre un issue en este repositorio.