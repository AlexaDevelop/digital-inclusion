# Inclusión Digital Blog

Proyecto web estático con enfoque en **inclusión digital**, diseñado como un mini‑blog/landing de múltiples secciones (Landing, Parte 1, Parte 2 y Parte 3) usando **HTML + Tailwind (CDN)** y algunas funciones JavaScript para cambiar de vista sin recargar la página.

> 💡 La página es _single file_ (un `index.html`) y se puede publicar fácilmente en **GitHub Pages**.

---

## ✨ Características

- **UI responsiva** con Tailwind CDN.
- Navegación interna sin router: secciones **Landing**, **Parte 1**, **Parte 2**, **Parte 3**.
- Componentes reutilizables (cards, banners, grids).
- Paleta institucional (**UNIMINUTO**) definida en CSS.
- Imágenes servidas desde **Google Drive** con el endpoint `thumbnail`.
- Enfoque básico de **accesibilidad** (uso de `alt`, `role="img"`, `aria-label`).

---

## 🗂️ Estructura sugerida

Aunque el proyecto funciona con un único archivo, se recomienda esta estructura para crecer ordenadamente:

```
.
├─ index.html
├─ assets/
│  ├─ img/           # (opcional si dejas de usar Drive)
│  ├─ css/           # estilos adicionales
│  └─ js/            # scripts si separas el JS del HTML
└─ README.md
```

> Actualmente Tailwind se carga por CDN en el `<head>` y el contenido de cada “post” se declara como _template string_ dentro de `<script>`.

---

## 🚀 Ejecutar localmente

No requiere servidor. Abre `index.html` en tu navegador.  
Si prefieres un servidor estático:

```bash
# Con Python 3
python -m http.server 8080
# abre http://localhost:8080
```

---

## 🌐 Despliegue en GitHub Pages

1. Crea un repositorio público en GitHub.
2. Sube `index.html` (y la carpeta `assets/` si la usas).
3. Ve a **Settings → Pages**.
4. En **Build and deployment**, selecciona:
   - **Source:** *Deploy from a branch*
   - **Branch:** `main`
   - **Folder:** `/ (root)`
5. Guarda. GitHub generará la URL del sitio (ej. `https://AlexaDevelop.github.io/digital-inclusion/`).

> Si usas un **sitio de usuario**, nombra el repo como `AlexaDevelop.github.io` para que la URL sea `https://AlexaDevelop.github.io/`.

---

## 🖼️ Imágenes con Google Drive

El proyecto usa el endpoint de **thumbnail** de Drive:

```
https://drive.google.com/thumbnail?id=ID_DEL_ARCHIVO&sz=w1600
```

- Asegúrate de que la imagen esté compartida como **“Cualquier persona con el enlace → Lector”**.
- Ajusta `sz` para la resolución (p. ej. `w1600`, `w2000`).
- Para **fondos que llenen** el contenedor (posible recorte):  
  `class="bg-center bg-no-repeat bg-cover"`
- Para **mostrar la imagen completa** (sin recorte, con bandas si no coincide la proporción):  
  `class="bg-center bg-no-repeat bg-contain"`

**Ejemplo (fondo que llena):**
```html
<div class="h-48 rounded-xl shadow-lg bg-center bg-no-repeat bg-cover"
     style="background-image:url('https://drive.google.com/thumbnail?id=ABC123&sz=w1600');">
</div>
```

**Ejemplo (imagen completa con proporción controlada):**
```html
<div class="rounded-xl overflow-hidden">
  <div class="w-full aspect-[4/5] bg-center bg-no-repeat bg-contain"
       style="background-image:url('https://drive.google.com/thumbnail?id=ABC123&sz=w1600');">
  </div>
</div>
```

> Alternativa `<img>` (semántica/SEO):  
> `https://drive.google.com/uc?export=view&id=ABC123` + `class="w-full h-auto"`

---

## 🎨 Paleta y utilidades

Colores definidos en CSS dentro del mismo archivo:

| Token                    | Hex      | Uso rápido                                  |
|--------------------------|----------|----------------------------------------------|
| `--uniminuto-blue`       | `#003E7E` | `bg-uniminuto-blue`, `color-uniminuto-blue` |
| `--uniminuto-yellow`     | `#F6AE2D` | `bg-uniminuto-yellow`, `color-uniminuto-yellow` |

```css
.color-uniminuto-blue { color: #003E7E; }
.color-uniminuto-yellow { color: #F6AE2D; }
.bg-uniminuto-blue { background-color: #003E7E; }
.bg-uniminuto-yellow { background-color: #F6AE2D; }
```

---

## 🧭 Cómo editar el contenido

### Agregar una nueva “Parte”
1. Duplica uno de los bloques `const postXContent = \`...\`;` y renómbralo (ej. `post4Content`).
2. Agrega un botón en `#blog-buttons`:
   ```html
   <button id="showPost4" class="font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 button-inactive">
     Parte 4
   </button>
   ```
3. En el script, añade:
   ```js
   const showPost4Btn = document.getElementById('showPost4');
   showPost4Btn.addEventListener('click', () => showPage('post4'));
   ```
4. Extiende `showPage(pageId)` con un nuevo `else if (pageId === 'post4') { ... }`.

### Cambiar imágenes
- Sustituye el `id` en los `thumbnail` o cambia a `<img>` si prefieres.
- Para **nitidez**, usa `sz` alto (ej. `w1600`+) y contenedores con `rounded-xl`/`shadow-lg`.

### Ajustar proporciones
- Usa `aspect-[ANCHO/ALTO]` (Tailwind) para mantener la relación del arte, por ejemplo `aspect-[16/9]`, `aspect-[4/5]`.

---

## ♿ Accesibilidad & SEO

- Siempre añade `alt` en `<img>`.  
- Cuando uses `background-image`, incorpora `role="img"` y `aria-label` en el contenedor.  
- Considera añadir `<meta name="description" content="...">` y un favicon.

---

## 🧰 Tecnologías

- **HTML5**, **Tailwind CSS (CDN)**, **JavaScript** nativo.
- Hosting: **GitHub Pages**.
- Imágenes: **Google Drive (thumbnail/uc)**.

---

## ✅ Roadmap (ideas)

- Separar JS en `assets/js/app.js`.
- Componente de posts reutilizable (registrar vistas dinámicamente).
- Carga perezosa (`loading="lazy"`) en `<img>`.
- Migrar imágenes de Drive a `assets/img/` para evitar dependencias externas.

---

## 📄 Licencia

Este proyecto es de uso educativo. Adáptalo libremente; si publicas, agrega créditos a **UNIMINUTO** y a la autora del contenido del blog.

---

## 📬 Contacto

Agrega aquí tus enlaces (correo, LinkedIn, etc.) y la **URL pública de GitHub Pages** una vez desplegado.
