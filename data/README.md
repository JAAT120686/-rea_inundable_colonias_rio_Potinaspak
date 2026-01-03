# 📊 Datos Geoespaciales

Esta carpeta contiene los archivos GeoJSON exportados desde QGIS que alimentan el mapa web interactivo.

## 📁 Archivos Incluidos

### areas_inundables.geojson
Polígonos que representan las zonas de riesgo de inundación clasificadas por nivel:
- **Alto riesgo**: Zonas con historial de inundaciones frecuentes
- **Riesgo medio**: Zonas con riesgo moderado
- **Riesgo bajo**: Zonas con riesgo mínimo

**Propiedades:**
- `nombre`: Identificador de la zona
- `riesgo`: Nivel de riesgo (alto, medio, bajo)
- `descripcion`: Información detallada sobre la zona

### rio.geojson
Línea que representa el cauce del Río Potinaspak.

**Propiedades:**
- `nombre`: Nombre del río
- `tipo`: Tipo de cuerpo de agua
- `descripcion`: Información sobre el río

### colonias.geojson
Polígonos que representan los límites de las colonias afectadas.

**Propiedades:**
- `nombre`: Nombre de la colonia
- `poblacion`: Población estimada
- `descripcion`: Información adicional

## 🔄 Actualización de Datos

Para actualizar los datos del mapa:

1. Exporta tus capas desde QGIS siguiendo las instrucciones en `/docs/INSTRUCCIONES_QGIS.md`
2. Reemplaza los archivos correspondientes en esta carpeta
3. Haz commit y push de los cambios

```bash
git add data/*.geojson
git commit -m "Actualizar datos geoespaciales"
git push origin main
```

## 📏 Formato y Estándares

- **Formato**: GeoJSON (RFC 7946)
- **Sistema de Coordenadas**: WGS 84 (EPSG:4326)
- **Codificación**: UTF-8
- **Precisión de coordenadas**: 6 decimales

## 📝 Notas

Los archivos de ejemplo incluidos en este directorio contienen datos demostrativos. 
**Reemplázalos con tus datos reales exportados desde QGIS.**

Las coordenadas de ejemplo están centradas en Ciudad de México y deben ser ajustadas 
a la ubicación real del Río Potinaspak y las colonias correspondientes.
