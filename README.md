# Plantilla Restaurante

Plantilla web completa para restaurantes, basada en el proyecto TOT PIZZA. Un solo archivo (`index.html`), sin dependencias ni build: se abre en el navegador y funciona.

## Qué incluye

- **Secciones:** Hero · Menú diario · Banner destacado · Carta · Sobre nosotros · Galería · Ubicación (mapa) · Reseñas · Contacto (formulario WhatsApp) · Footer
- **4 idiomas:** ES / CA / EN / FR con selector en la cabecera
- **Panel de administración** (`#admin` en la URL): edita textos, carta, menú diario, horarios, colores, galería, contacto y visibilidad de secciones
- **Panel del dueño:** acceso restringido que solo permite editar el menú diario
- **Seguridad:** PINs con hash SHA-256 (nunca en claro), bloqueo de 5 min tras 5 intentos fallidos
- **Persistencia:** localStorage por defecto; sincronización entre dispositivos opcional vía JSONBin (se configura desde el panel, pestaña General)
- **SEO:** meta tags, Open Graph, Twitter Cards y schema.org listos para rellenar

## Códigos de acceso por defecto

| Código | Rol | Acceso |
|---|---|---|
| `admin1234` | Administrador | Todo el panel |
| `dueno1234` | Dueño | Solo menú diario |

Entra añadiendo `#admin` a la URL. **Cambia ambos códigos** desde Panel → General antes de entregar la web.

## Cómo personalizar para un restaurante nuevo

1. **Copia esta carpeta** con el nombre del proyecto.
2. **Desde el panel de admin** (lo más rápido): nombre, textos del hero, carta completa, menú diario, horarios, dirección, WhatsApp, Instagram, colores y fotos de la galería.
3. **En el código** (buscar `EDITAR`):
   - `<head>`: title, description, keywords, canonical, Open Graph y el bloque schema.org
   - Banner destacado: textos `sgTitle` / `sgText` en `TRANSLATIONS` (4 idiomas)
   - Reseñas: bloque `<!-- TESTIMONIOS -->` con reseñas reales y el enlace a Google Maps
   - Enlace "Cómo llegar": sustituir `DIRECCION+DEL+RESTAURANTE`
4. **Idiomas:** los textos de la interfaz están en `TRANSLATIONS` (es/ca/en/fr). Las traducciones de platos en `MENU_T` (clave = id del plato en `DEFAULTS.menu`). El español es el idioma canónico: lo que se edita en el panel se muestra en ES; el resto de idiomas usa las traducciones fijas del código.
5. **Logo:** la plantilla usa el emoji 🍽️. Para poner un logo real, busca `class="dot"` (cabecera, footer, paneles) y el `<link rel="icon">` del head — en el proyecto TOT PIZZA tienes el ejemplo de cómo queda con imágenes.
6. **Lista de ingredientes** (opcional, para pizzerías o similares): rellena `DEFAULTS.menuIngredients` y añade `ingList` a cada idioma en `TRANSLATIONS`. Si está vacío, el recuadro no se muestra.

## Notas técnicas

- Claves de localStorage con prefijo `resto_` (no chocan con otras webs de la misma plantilla en el mismo dominio... si alojas dos, cambia el prefijo).
- Si cambias la carta o el menú diario en `DEFAULTS` directamente en el código y el navegador "no se entera", es por datos viejos en localStorage: sube `menuV` o `daily.v` en `DEFAULTS` para forzar la actualización.
- Los PINs se guardan como hash SHA-256 con salt (`_S` en el código). Para generar el hash de un PIN nuevo por código: `sha256(salt + pin)`. Desde el panel se hace solo.
