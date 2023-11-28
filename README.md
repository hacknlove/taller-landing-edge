# Taller Landing Edge

En este taller, vamos a aprender a hacer una landing page y a desplegarla en el edge.

## Conceptos iniciales:
**Landing page:** Es una página web que tiene como objetivo captar la atención de un usuario y llevarlo a realizar una acción determinada. Por ejemplo, suscribirse a un newsletter, descargar un ebook, comprar un producto, etc.

Se llama landing page porque es la página a la que llega un usuario después de hacer click en un enlace, ya sea de un anuncio, un email, un post en redes sociales, etc.

**Edge:** Es un servidor que se encuentra en la red de distribución de contenidos (CDN) más cercano al usuario final. Su objetivo es servir el contenido de la página web de la forma más rápida posible.

## Preparativos:

### Instalar herramientas

1. Instalar [Visual Studio Code](https://code.visualstudio.com/). (Opcional. Puedes usar el IDE que prefieras)
2. Instalar git
3. Instalar [Node.js](https://nodejs.org/es/)

### Preparar entorno de desarrollo

#### Clonar este repositorio
```bash
git clone https://github.com/hacknlove/taller-landing-edge.git

cd taller-landing-edge
```

#### Crear Proyecto con Astro

```bash
npm create astro@latest

cd mi-landing
```

Respuestas:

* **Install Astro:** Yes
* **Where should we create your new project?** mi-landing
* **How would you like to start your new project?** Include sample files
* **Install dependencies?** Yes
* **Do you plan to write TypeScript?** No
* **Initialize a new git repository?** No

### Compartir nuestro proyecto

Para que todos podamos ver la web de todos, vamos a ejecutar los entornos de desarrollo en modo host.

Para ello, vamos a modificar el archivo `mi-landing.json` y añadir ` --host` al script `dev`

Quedará así:
    
```json
"dev": "astro dev --host",
```

### Lanzar el entorno de desarrollo

```bash
cd mi-landing
npm run dev
```

Debemos ver algo así:

```
> landing-edge@0.0.1 dev
> astro dev --host

  🚀  astro  v3.0.13 started in 98ms
  
  ┃ Local    http://localhost:4321/
  ┃ Network  http://192.168.1.132:4321/
```

Si abrimos la url `http://localhost:4321/` en nuestro navegador, veremos la web de nuestro proyecto.

Cualquiera que se encuentre en la misma red, podrá ver nuestra web en la url `http://<nuestra-ip-local>:4321/` (en el ejemplo anterior, `http://192.168.1.132:4321/`)

## Introducción Astro

Echando un vistazo a los archivos de nuestro proyecto `mi-landing/src`, podemos ver:

* `pages/`
* `components/`
* `layouts/`

`pages/` es el único directorio que tiene una función y un significado definido por astro. Las otras carpetas son solo convenciones de nombres que se usan para organizar el resto del código. Cada cual puede organizar su código como quiera.

`pages/` es el directorio donde se encuentran las páginas de nuestra web. Cada archivo `.astro` en este directorio se convierte en una página de nuestra web.

Por lo tanto `pages/index.astro` es la página principal de nuestra web.

Si abrimos el archivo `pages/index.astro` podemos ver que se parece mucho un archivo html normal, con las siguientes diferencias:

* Lleva un encabezado en javascript que define el contexto
```
---
import Layout from '../layouts/Layout.astro';
import Card from '../components/Card.astro';
---
```

En este caso está importando dos componentes.

* El html que sigue, es realmente JSX. Podemos usar componentes, y podemos interpolar expresiones de javascript.

* El tag `style` solo se aplicará a la página o componente en el que se encuentre.

Si abrimos el archivo `layouts/Layout.astro` podemos ver cómo la propiedad title que se pasa en `index.astro` como `<Layout title="">...` se obtiene usando la variable global `Astro` como `const { title } = Astro.props;` (`const title = Astro.props.title`)

Vemos también que el contenido que le pasamos a `Layout` se renderiza en el tag `slot`.

Y vemos también que el tag `style` usa la directiva `is:global` para definir que el estilo se aplicará a todos los componentes y páginas.

En `components/Card.astro` no hay nada nuevo.

De momento, estas son las únicas cosas que necesitamos saber de Astro para hacer nuestra landing page.

## Hacer nuestra landing page

Vamos a hacer una landing page para el paraisu.

Tendrá los siguientes elementos:
1. Background 
2. Descripción
3. CTA

### Limpiar el proyecto

Vamos a borrar todo lo que no necesitamos.

Ve a `layouts/Layout.astro` y limpia style.

```html
<style is:global>
	html {
		background: #000;
		color: #fff;
        margin: 0;
        padding: 0;
    }
    body {
        margin: 0;
        padding: 0;
    }
</style>
```

Ve a `pages/index.astro` y deja solo el layout.

```astro
---
import Layout from '../components/Layout.astro';
---

<Layout title="Paraisu to Astro.">
</Layout>
```

Elimina el archivo `components/Card.astro`

### Background

Crea un archivo `components/Background.astro` y añade el siguiente contenido:

```astro
<div>
    ES EL BACKGROUND
</div>
```

Edita `pages/index.astro` y añade el componente `Background`:

```astro
---
import Background from '../components/Background.astro';
import Layout from '../layouts/Layout.astro';
---

<Layout title="Welcome to Astro.">
    <Background />
</Layout>
```

La idea es añadir un componente "vacío", e ir iterando sobre él, viendo los cambios
