# Selector Laboral PWA v1.0

Aplicación estática en español para iPhone y navegadores modernos. No requiere Python en el iPhone.

## Instalación en iPhone

1. Publica **todos** los archivos de esta carpeta en un hosting HTTPS estático (por ejemplo, GitHub Pages, Netlify o Cloudflare Pages). No basta abrir `index.html` desde Archivos del iPhone: para instalar la PWA y activar el modo sin conexión se necesita HTTPS.
2. En iPhone abre la URL publicada en **Safari**.
3. Pulsa **Compartir** → **Agregar a pantalla de inicio** → **Agregar**.
4. Abre «Selector Laboral» desde la pantalla de inicio. Una vez cargada, puede abrirse sin conexión para revisar ofertas guardadas.

### Publicación sencilla con GitHub Pages

Crea un repositorio público nuevo en GitHub, carga el contenido de esta carpeta en la raíz, y en Settings → Pages selecciona Deploy from a branch, `main` y `/ (root)`. Espera a que GitHub muestre la URL HTTPS. **Atención:** un repositorio público publica el código y cualquier archivo incluido; nunca subas datos personales, contraseñas ni ofertas privadas. La app almacena las ofertas del usuario en su propio navegador, no en el repositorio.

## Uso

- Pulsa **Agregar oferta** para registrar un aviso, o importa `ejemplo_ofertas.csv` para probar el ranking.
- Acepta CSV con cabeceras `title,company,source,location,description,url,date` (también `cargo,empresa,portal,ubicacion,descripcion,enlace,fecha`). El delimitador CSV es coma, y los campos con comas deben ir entre comillas. Acepta JSON como lista de objetos o `{ "ofertas": [...] }`.
- Las puntuaciones se calculan mediante reglas heurísticas ponderadas; **no son un análisis semántico de IA**. Verifica requisitos obligatorios manualmente. Los ejemplos son ficticios.
- **Exportar CSV** genera un ranking abrible en Excel; **Respaldo JSON** permite conservar e importar los registros y su estado. Se recomienda respaldar regularmente.
- La app conserva los datos en `localStorage` del navegador/dispositivo. Borrar los datos de Safari o cambiar de teléfono puede eliminarlos. No hay sincronización entre dispositivos en esta versión.

## Servidor futuro

En Configuración, escribe un endpoint HTTPS que responda `GET` con un JSON `[{"title":"...","company":"...","description":"...","source":"...","location":"...","url":"...","date":"YYYY-MM-DD"}]` o `{ "ofertas": [...] }`. Debe permitir CORS desde el dominio de la PWA. El botón **Sincronizar ofertas** obtiene y deduplica los registros. No almacenes tokens secretos en JavaScript cliente. Para autenticar, se necesita una arquitectura segura de servidor.

La recolección de ofertas debe realizarse mediante APIs autorizadas, alertas por correo con consentimiento o archivos exportados, respetando las condiciones de cada portal. **Esta PWA no hace scraping ni búsqueda automática programada**. Para 09:00 y 18:00 se necesita un backend/scheduler externo.

## Limitaciones

- No incluye ofertas reales ni acceso directo a Computrabajo, LinkedIn, Chiletrabajos, Indeed o Trabajando.com.
- Deduplicación por URL canónica aproximada (dominio y ruta), o por cargo + empresa + ubicación cuando no hay URL. Puede requerir revisión manual de duplicados.
- La fecha de publicación no se verifica.
- No se ha publicado a un dominio; necesitas hosting HTTPS para instalarla en iPhone.
