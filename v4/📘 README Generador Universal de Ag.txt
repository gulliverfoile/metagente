README: Generador Universal de Agentes (v2.0 – Hexagonal Edition)
Un motor genérico en JavaScript puro (un solo archivo HTML) para crear agentes conversacionales sin programar.
Solo necesitas un archivo agente.json describiendo el dominio (recetas, películas, ejercicios, viajes…) y la aplicación genera automáticamente:

Un chat que entiende lenguaje natural básico (basado en sinónimos).

Filtros dinámicos para refinar búsquedas.

Lista de resultados con valoraciones (👍/👎) y favoritos ⭐.

Persistencia de preferencias por agente (localStorage).

Caché de datos externos mediante IndexedDB (para conjuntos de datos grandes).

Arquitectura interna hexagonal (componentes desacoplados, EventBus, estado centralizado).

🚀 ¿Qué hace exactamente?
Carga la definición del agente desde un JSON (subido por el usuario o el ejemplo precargado).

Obtiene los datos de una de estas fuentes:

dataSource.type = "local" → datos incrustados en el JSON.

dataSource.type = "remote" → descarga JSON/CSV (con caché automática en IndexedDB, versión controlada).

Compatibilidad hacia atrás con "datos": [...] (JSON antiguos).

Construye dinámicamente la interfaz:

Panel de filtros (selectores, rangos numéricos, checkboxes de tags) según los atributos definidos.

Tarjetas de resultados mostrando los atributos marcados como visible.

Chat que interpreta frases usando el diccionario de sinónimos.

Gestiona preferencias por agente: valoraciones (like/dislike) y lista de favoritos, guardadas en localStorage.

Funciona offline tras la primera carga de datos remotos (gracias a IndexedDB).

🧠 ¿Cómo lo hace? (Arquitectura interna)
A diferencia de la versión anterior (todo mezclado), ahora sigue principios hexagonales dentro del propio HTML:

Capa / Componente	Responsabilidad
EventBus	Mensajero central. Los componentes solo emiten y escuchan eventos, nunca se tocan directamente.
PersistenceService	Encapsula IndexedDB (caché de datasets) y localStorage (preferencias, modo oscuro).
AgentEngine (lógica pura)	Filtrado, ordenación, procesamiento de sinónimos. Sin DOM, sin dependencias externas.
AppState	Único almacén de estado (agente cargado, filtros, watchlist, valoraciones).
Componentes UI (ChatUI, FilterUI, ResultListUI, ModalUI)	Cada uno maneja su trozo de DOM, escucha eventos del bus y emite acciones.
App	Orquestador: cablea el bus, los servicios y la UI. Maneja el ciclo de vida.
Flujo típico de una interacción:

Usuario escribe en el chat → ChatUI emite chat:message.

App recibe el evento, llama al motor de sinónimos (AgentEngine) y actualiza el estado.

El estado emite state:filtersChanged → FilterUI se redibuja.

Se aplican filtros → state:resultsUpdated → ResultListUI se redibuja.

Ningún componente sabe de la existencia de los otros. Si mañana añades una entrada por voz, solo tocas ChatUI o creas un adaptador nuevo.

📦 Estructura del archivo agente.json
Ejemplo completo (recetas, con pulpo á feira incluido):

json
{
  "meta": {
    "nombre": "NutriAgente Recetas",
    "descripcion": "Recomendaciones de cocina con filtros inteligentes (y pulpo á feira bajo en calorías)",
    "version": "1.0"
  },
  "atributos": [
    { "id": "nombre", "nombre": "Nombre", "tipo": "texto", "visible": true, "filtrable": false },
    { "id": "categoria", "nombre": "Categoría", "tipo": "categoria", "opciones": ["Desayuno","Comida","Cena","Snack"], "visible": true, "filtrable": true },
    { "id": "tiempo", "nombre": "Tiempo (min)", "tipo": "numero", "visible": true, "filtrable": true },
    { "id": "precio", "nombre": "Precio (€)", "tipo": "numero", "visible": true, "filtrable": true },
    { "id": "calorias", "nombre": "Calorías", "tipo": "numero", "visible": true, "filtrable": true },
    { "id": "dieta", "nombre": "Dieta", "tipo": "tags", "opciones": ["Vegetariano","Sin gluten","Sin lactosa"], "visible": true, "filtrable": true }
  ],
  "dataSource": {
    "type": "local",
    "data": [
      { "id":1, "nombre":"Avena nocturna", "categoria":"Desayuno", "tiempo":5, "precio":1.2, "calorias":320, "dieta":["Vegetariano","Sin gluten"] },
      { "id":2, "nombre":"Pulpo á feira", "categoria":"Cena", "tiempo":30, "precio":5.0, "calorias":150, "dieta":["Sin gluten"] },
      { "id":3, "nombre":"Ensalada César", "categoria":"Comida", "tiempo":10, "precio":3.5, "calorias":280, "dieta":["Sin lactosa"] }
    ]
  },
  "sinonimos": {
    "tiempo": { "rápido":[0,10], "normal":[10,20], "lento":[20,60] },
    "precio": { "barato":[0,2], "económico":[0,2.5], "caro":[3,10] },
    "categoria": { "desayuno":"Desayuno", "comida":"Comida", "cena":"Cena" }
  }
}
Campos importantes
meta: nombre y descripción (se muestran al cargar).

atributos: define las propiedades de los ítems. Cada uno tiene:

id: clave en los datos.

tipo: texto, categoria, numero, tags, url, boolean.

visible: si se muestra en la tarjeta de resultado.

filtrable: si aparece en el panel de filtros.

opciones: (solo categoria o tags) valores posibles.

dataSource (recomendado):

type: "local" → data contiene el array de ítems.

type: "remote" → url apunta a un JSON o CSV externo, y version controla la caché.

datos (compatible con JSON antiguos): array directo si no usas dataSource.

sinonimos: mapea palabras del chat a valores de filtro. Pueden ser:

Categoría: "desayuno": "Desayuno".

Rango numérico: "barato": [0, 2].

Tags: "vegetariano": ["Vegetariano"].

🤖 Prompt para que una IA te genere el JSON
Copia y pega esto en ChatGPT, Claude o similar:

text
Quiero que actúes como generador de agentes para el "Generador Universal de Agentes". Debes generar un JSON válido siguiendo el esquema. El agente será sobre [DESCRIBE TU DOMINIO: ej. "recomendación de películas"].

Incluye:
- meta: nombre y descripción.
- atributos: al menos 4, con tipos variados (categoria, numero, tags). Cada uno con id (minúsculas, sin espacios), nombre, tipo, visible (true) y filtrable (true excepto el nombre). Para categoría y tags, añade opciones.
- dataSource: type "local" con data: al menos 5 ejemplos realistas.
- sinonimos: al menos 3 mapeos (ej. "barato" a rango, "rápido" a tiempo, "familiar" a categoría).

Devuelve SOLO el JSON válido, sin explicaciones.
🖥️ Cómo usar la aplicación
Guarda el código HTML en un archivo index.html.

Ábrelo con cualquier navegador moderno (doble clic).

Haz clic en 📂 Cargar agente (JSON) y selecciona tu archivo agente.json.

O prueba con el botón 📥 Cargar agente de ejemplo (recetas con pulpo).

Una vez cargado:

Escribe en el chat (ej. "algo rápido y barato").

Usa los filtros manualmente si lo prefieres.

Valora ítems con 👍/👎 y guárdalos en ⭐ favoritos.

Tus preferencias se guardan automáticamente para ese agente.

Si el agente usa datos remotos, la primera carga puede tardar unos segundos (descarga + cache). Luego será instantánea.

⚠️ Limitaciones conocidas
Los datos externos deben estar en servidores con CORS permitido (GitHub raw, Netlify, Vercel…).

El tamaño de caché en IndexedDB depende del navegador, pero soporta cientos de MB sin problema.

El chat es procesamiento de sinónimos, no IA generativa. Suficiente para dominios pequeños y bien definidos.

Es 100% local: sin backend, sin autenticación, sin compartir en nube.

🧠 Mejoras futuras (posibles)
Añadir dataSource.type = "api" con paginación y búsqueda en tiempo real.

Editor visual de atributos para crear agentes sin tocar JSON.

Exportar/importar agente completo (datos cacheados incluidos).

Sugerencias en el chat (autocompletado basado en el dataset).

Adaptadores de entrada adicionales (voz, gestos) sin cambiar el núcleo, solo añadiendo emisores de eventos.
