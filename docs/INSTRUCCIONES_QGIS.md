# 📘 Guía Detallada: Exportar Mapas de QGIS para Visualización Web

Esta guía proporciona instrucciones paso a paso para exportar tus mapas de QGIS y publicarlos en este repositorio.

## 🎯 Objetivo

Exportar capas de QGIS en formato GeoJSON para que puedan ser visualizadas en el mapa web interactivo del repositorio.

## 📋 Requisitos Previos

- QGIS 3.x instalado
- Proyecto de QGIS con las capas que deseas publicar
- Conocimientos básicos de Git (opcional, pero recomendado)

## 🔧 Paso a Paso

### 1. Preparar el Proyecto en QGIS

#### 1.1 Verificar el Sistema de Coordenadas

Para mapas web, es esencial usar el sistema de coordenadas WGS 84 (EPSG:4326):

1. Abre tu proyecto en QGIS
2. Ve a **Proyecto** → **Propiedades** → **SRC**
3. Verifica que el SRC del proyecto sea **EPSG:4326 - WGS 84**
4. Si no lo es, puedes cambiarlo, pero es mejor reproyectar las capas individualmente

#### 1.2 Reproyectar Capas (si es necesario)

Si tus capas están en otro sistema de coordenadas:

1. Haz clic derecho en la capa → **Exportar** → **Guardar objetos como...**
2. En "SRC", selecciona **EPSG:4326 - WGS 84**
3. Guarda temporalmente la capa reproyectada
4. Reemplaza la capa original con la reproyectada

#### 1.3 Organizar y Nombrar Capas

1. Renombra tus capas con nombres descriptivos:
   - `areas_inundables` para zonas de riesgo
   - `rio` para el cauce del río
   - `colonias` para los límites de colonias
2. Ordena las capas en el panel de capas de arriba (más visible) a abajo

### 2. Configurar Atributos de las Capas

Para que el mapa web muestre información útil, tus capas deben tener atributos apropiados:

#### 2.1 Atributos Recomendados

Para **áreas inundables**:
- `nombre`: Nombre de la zona
- `riesgo`: Nivel de riesgo (`alto`, `medio`, `bajo`)
- `descripcion`: Descripción detallada

Para **río**:
- `nombre`: Nombre del río
- `tipo`: Tipo de cuerpo de agua
- `descripcion`: Información adicional

Para **colonias**:
- `nombre`: Nombre de la colonia
- `poblacion`: Población estimada (opcional)
- `descripcion`: Información relevante

#### 2.2 Agregar o Editar Atributos

1. Abre la tabla de atributos: Clic derecho en la capa → **Abrir tabla de atributos**
2. Activa el modo de edición: Clic en el ícono del lápiz
3. Agrega campos si es necesario: **Calculadora de campos** o **Nuevo campo**
4. Edita los valores según corresponda
5. Guarda los cambios: Clic en el ícono del disquete

### 3. Exportar a GeoJSON

#### 3.1 Exportar una Capa

Para cada capa que quieras incluir en el mapa web:

1. Haz clic derecho en la capa → **Exportar** → **Guardar objetos como...**

2. Configura las opciones de exportación:
   - **Formato:** GeoJSON
   - **Nombre de archivo:** Elige un nombre descriptivo (ej: `areas_inundables.geojson`)
   - **SRC:** EPSG:4326 - WGS 84
   - **Codificación:** UTF-8

3. Opciones avanzadas (haz clic en "Opciones de capa"):
   - **Precisión de coordenadas:** 6 (suficiente para la mayoría de los casos)
   - **RFC7946:** Marca esta opción para mejor compatibilidad con estándares web

4. Haz clic en **Aceptar**

5. Guarda el archivo en la carpeta `data/` de tu repositorio local

#### 3.2 Exportar Múltiples Capas

Si tienes varias capas, repite el proceso para cada una:

```
data/
├── areas_inundables.geojson
├── rio.geojson
└── colonias.geojson
```

### 4. Optimizar los Archivos GeoJSON

Los archivos GeoJSON pueden ser grandes. Aquí hay algunas formas de optimizarlos:

#### 4.1 Simplificar Geometría

Si tus polígonos son muy detallados:

1. Ve a **Vectorial** → **Geometría** → **Simplificar**
2. Elige un valor de tolerancia (empieza con 0.0001)
3. Previsualiza el resultado
4. Exporta la capa simplificada

#### 4.2 Reducir Atributos

Elimina campos que no necesitas en el mapa web:

1. En la ventana de exportación, expande **Seleccionar campos a exportar**
2. Desmarca los campos innecesarios
3. Mantén solo `nombre`, `riesgo`, `descripcion` y otros relevantes

### 5. Verificar los Archivos Exportados

#### 5.1 Verificar Formato JSON

Abre el archivo `.geojson` en un editor de texto y verifica que tenga esta estructura:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "nombre": "Colonia Centro",
        "riesgo": "alto",
        "descripcion": "Zona con alto riesgo de inundación"
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[...]]]
      }
    }
  ]
}
```

#### 5.2 Validar en un Visualizador Online

Antes de publicar, verifica tus archivos en:
- [geojson.io](http://geojson.io/)
- [geojsonlint.com](https://geojsonlint.com/)

### 6. Actualizar el Mapa Web

#### 6.1 Ajustar el Centro del Mapa

1. Abre `index.html` en un editor de texto
2. Busca la línea que contiene `L.map('map').setView`
3. Obtén las coordenadas del centro de tu área de interés en QGIS:
   - Haz clic en un punto central con la herramienta de información
   - Copia las coordenadas (latitud, longitud)
4. Actualiza las coordenadas en `index.html`:

```javascript
var map = L.map('map').setView([19.4326, -99.1332], 13);
//                                 ↑ lat     ↑ lon   ↑ zoom
```

#### 6.2 Verificar las Rutas de los Archivos

Si usaste nombres diferentes para tus archivos, actualiza las rutas en `index.html`:

```javascript
loadGeoJSON('data/areas_inundables.geojson', getStyle, onEachFeature);
loadGeoJSON('data/rio.geojson', getStyle, onEachFeature);
loadGeoJSON('data/colonias.geojson', getStyle, onEachFeature);
```

### 7. Publicar en el Repositorio

#### 7.1 Usando Git (Línea de Comandos)

```bash
# Navega a tu repositorio local
cd /ruta/a/-rea_inundable_colonias_rio_Potinaspak

# Agrega los archivos nuevos
git add data/*.geojson
git add index.html

# Verifica qué archivos se van a commit
git status

# Haz commit de los cambios
git commit -m "Agregar mapas exportados desde QGIS"

# Sube los cambios al repositorio
git push origin main
```

#### 7.2 Usando GitHub Desktop

1. Abre GitHub Desktop
2. Verifica que los archivos aparezcan en la lista de cambios
3. Escribe un mensaje de commit descriptivo
4. Haz clic en "Commit to main"
5. Haz clic en "Push origin"

#### 7.3 Subir Archivos Directamente por Web

Si no usas Git:

1. Ve a tu repositorio en GitHub
2. Navega a la carpeta `data/`
3. Haz clic en "Add file" → "Upload files"
4. Arrastra tus archivos `.geojson`
5. Escribe un mensaje de commit
6. Haz clic en "Commit changes"

### 8. Activar GitHub Pages

Para que tu mapa sea visible en línea:

1. Ve a tu repositorio en GitHub
2. Haz clic en **Settings** (Configuración)
3. En el menú lateral, selecciona **Pages**
4. En "Source", selecciona la rama **main** y carpeta **/ (root)**
5. Haz clic en **Save**
6. Espera unos minutos
7. Tu mapa estará disponible en: `https://JAAT120686.github.io/-rea_inundable_colonias_rio_Potinaspak/`

## 🎨 Personalización Avanzada

### Cambiar Colores por Nivel de Riesgo

En `index.html`, busca la función `getStyle` y modifica los colores:

```javascript
case 'alto':
    color = 'rgba(255, 0, 0, 0.5)';  // Rojo
    break;
case 'medio':
    color = 'rgba(255, 165, 0, 0.5)';  // Naranja
    break;
case 'bajo':
    color = 'rgba(255, 255, 0, 0.5)';  // Amarillo
    break;
```

### Agregar Más Información al Popup

Modifica la función `onEachFeature` para mostrar más campos:

```javascript
if (feature.properties.poblacion) {
    popupContent += '<p><strong>Población:</strong> ' + feature.properties.poblacion + '</p>';
}
```

## ❓ Solución de Problemas

### El mapa no carga las capas

- Verifica que los archivos `.geojson` estén en la carpeta `data/`
- Abre la consola del navegador (F12) y busca errores
- Verifica que las rutas en `index.html` coincidan con los nombres de archivo

### Las coordenadas se ven incorrectas

- Verifica que el SRC sea EPSG:4326
- Asegúrate de que el formato de coordenadas sea [latitud, longitud]

### El archivo GeoJSON es muy grande

- Simplifica la geometría en QGIS
- Reduce el número de vértices
- Elimina atributos innecesarios

### El mapa está centrado en el lugar equivocado

- Actualiza las coordenadas en `L.map('map').setView([lat, lon], zoom)`
- Usa las coordenadas de un punto central de tu área de estudio

## 📚 Recursos Adicionales

- [Documentación de QGIS](https://docs.qgis.org/)
- [Especificación GeoJSON](https://geojson.org/)
- [Leaflet Documentation](https://leafletjs.com/)
- [Tutoriales de QGIS en español](https://www.qgistutorials.com/es/)

## 💡 Consejos

1. **Mantén archivos pequeños:** GeoJSON puede ser grande; simplifica geometrías cuando sea posible
2. **Usa nombres consistentes:** Facilita el mantenimiento del código
3. **Documenta tus datos:** Agrega descripciones claras en los atributos
4. **Prueba localmente primero:** Verifica que todo funcione antes de publicar
5. **Haz commits frecuentes:** Guarda versiones de tu trabajo regularmente

---

¿Tienes preguntas? Abre un issue en el repositorio.
