# 🚀 Guía de Publicación en GitHub Pages

Esta guía te ayudará a publicar tu mapa interactivo en línea usando GitHub Pages.

## 📌 ¿Qué es GitHub Pages?

GitHub Pages es un servicio gratuito de GitHub que te permite publicar sitios web estáticos directamente desde tu repositorio. Es ideal para visualizar mapas interactivos como el que has creado.

## 🔧 Configuración de GitHub Pages

### Paso 1: Acceder a la Configuración del Repositorio

1. Ve a tu repositorio en GitHub: https://github.com/JAAT120686/-rea_inundable_colonias_rio_Potinaspak
2. Haz clic en **Settings** (Configuración) en la parte superior del repositorio
3. En el menú lateral izquierdo, busca y haz clic en **Pages**

### Paso 2: Configurar la Fuente de Publicación

En la sección **Source** (Fuente):

1. Selecciona la rama **main** (o la rama donde están tus archivos)
2. Selecciona la carpeta **/ (root)** 
3. Haz clic en **Save** (Guardar)

### Paso 3: Esperar la Publicación

1. GitHub comenzará a construir tu sitio automáticamente
2. Este proceso puede tardar de 1 a 5 minutos
3. Verás un mensaje indicando que tu sitio está listo

### Paso 4: Acceder a tu Mapa

Una vez publicado, tu mapa estará disponible en:

**https://JAAT120686.github.io/-rea_inundable_colonias_rio_Potinaspak/**

## ✅ Verificar que Funciona

1. Abre la URL en tu navegador
2. Deberías ver el mapa con el título "Área Inundable Colonias Río Potinaspak"
3. El mapa debería cargar con las capas de datos (áreas inundables, río, colonias)
4. Prueba hacer zoom y click en las áreas para ver la información

## 🔄 Actualizar el Mapa

Cada vez que hagas cambios y los subas al repositorio:

```bash
git add .
git commit -m "Actualizar mapa"
git push origin main
```

GitHub Pages se actualizará automáticamente en 1-5 minutos.

## 🎨 Personalizar el Dominio (Opcional)

Si tienes un dominio propio, puedes configurarlo:

1. En la página de **Settings** → **Pages**
2. En la sección **Custom domain**, ingresa tu dominio
3. Configura los registros DNS según las instrucciones de GitHub

## 🛠️ Solución de Problemas

### El mapa no carga

- **Verifica**: Que GitHub Pages esté activado en Settings
- **Espera**: Al menos 5 minutos después de activar o hacer cambios
- **Revisa**: La consola del navegador (F12) para ver errores

### Las capas no se muestran

- **Verifica**: Que los archivos `.geojson` estén en la carpeta `data/`
- **Comprueba**: Que los nombres de archivo en `index.html` coincidan con los archivos reales
- **Valida**: Que los archivos GeoJSON sean válidos en http://geojson.io/

### El mapa está en el lugar equivocado

- Abre `index.html`
- Busca la línea con `L.map('map').setView([lat, lon], zoom)`
- Ajusta las coordenadas a tu ubicación real
- Guarda, haz commit y push

## 📱 Compartir el Mapa

Una vez publicado, puedes compartir el enlace con:

- Colegas y colaboradores
- Autoridades locales
- Comunidades afectadas
- Redes sociales

El mapa es responsivo y funciona en:
- 💻 Computadoras de escritorio
- 📱 Tablets
- 📱 Teléfonos móviles

## 🔒 Privacidad y Seguridad

### Repositorio Público
- Si tu repositorio es público, cualquiera puede ver el mapa
- Ideal para información que debe ser pública

### Repositorio Privado
- Con GitHub Pro/Team, puedes tener repositorios privados con Pages
- El mapa solo será accesible por personas con permisos

## 📊 Estadísticas de Uso

GitHub proporciona estadísticas básicas:

1. Ve a **Insights** en tu repositorio
2. Selecciona **Traffic** para ver:
   - Número de visitantes
   - Vistas de página
   - Repositorios que hacen referencia

## 🆘 Ayuda Adicional

- [Documentación oficial de GitHub Pages](https://docs.github.com/es/pages)
- [Guía de inicio rápido](https://docs.github.com/es/pages/getting-started-with-github-pages)
- [Solución de problemas](https://docs.github.com/es/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)

## ✨ Mejoras Futuras

Considera agregar:

- **Google Analytics**: Para rastrear visitantes
- **Búsqueda de direcciones**: Usando API de geocodificación
- **Capas adicionales**: Datos de precipitación, elevación, etc.
- **Exportar PDF**: Opción para descargar el mapa
- **Compartir en redes**: Botones para compartir en redes sociales

---

¿Necesitas ayuda? Abre un issue en el repositorio o consulta la documentación en `/docs/`.
