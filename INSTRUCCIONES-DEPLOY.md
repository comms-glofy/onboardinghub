# Glofy Onboarding Hub — Deploy en Netlify
## Instrucciones para Comms (sin IT, sin código)

---

## Antes de empezar, necesitás tener:
- Cuenta en **netlify.com** (gratis — registrate con tu mail de Glofy)
- La **Anthropic API key** (conseguila en console.anthropic.com → "API Keys" → "Create Key")

---

## Paso 1 — Subir el proyecto a Netlify

1. Ingresá a **netlify.com** y hacé login
2. En el dashboard, hacé click en **"Add new site"** → **"Deploy manually"**
3. Arrastrá la carpeta **`glofy-hub`** completa al área que dice *"Drag and drop your site folder here"*
4. Netlify va a subir todo automáticamente y te va a dar una URL del tipo:
   `https://nombre-aleatorio.netlify.app`

---

## Paso 2 — Configurar la API key (el paso clave de seguridad)

Una vez subido el sitio:

1. En el panel de tu sitio en Netlify, andá a **Site configuration → Environment variables**
2. Hacé click en **"Add a variable"**
3. Completá:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** *tu API key de Anthropic* (la que empieza con `sk-ant-...`)
4. Hacé click en **"Save"**
5. Volvé a **Deploys** y hacé click en **"Trigger deploy"** → **"Deploy site"**

La key queda guardada del lado del servidor. Ningún Glofer puede verla.

---

## Paso 3 — Verificar que funciona

1. Abrí la URL que te dio Netlify
2. El chatbot debería responder directamente, sin pedir ninguna key
3. Probá una pregunta de test: *"¿Cómo pido un day off?"*

---

## Paso 4 (opcional) — Cambiar la URL por un dominio propio

Si IT quiere que quede en `glofy.co/hub` en vez de en Netlify:
- Opción A: IT configura un redirect desde `glofy.co/hub` hacia la URL de Netlify
- Opción B: IT conecta el dominio `glofy.co` directamente en Netlify (Site configuration → Domain management)

Para la demo con gerencia, la URL de Netlify es suficiente.

---

## Estructura del proyecto (no modificar)

```
glofy-hub/
├── index.html              ← El sitio completo
├── netlify.toml            ← Configuración de Netlify
└── netlify/
    └── functions/
        └── chat.js         ← El proxy seguro (no tocar)
```

---

## Preguntas frecuentes

**¿Tiene algún costo?**
El plan gratuito de Netlify cubre ampliamente el volumen de uso del hub.
La API de Anthropic se cobra por uso (por tokens). Para el volumen de un onboarding interno, el costo es mínimo.

**¿Qué pasa si IT quiere migrar esto a glofy.co?**
Entregale la carpeta `glofy-hub` completa y estas instrucciones. El proceso en su servidor es equivalente: alojan los archivos, crean una variable de entorno `ANTHROPIC_API_KEY`, y listo.

**¿La API key es segura?**
Sí. Nunca aparece en el código del sitio. Vive en las variables de entorno de Netlify y solo se usa en el servidor, invisible para cualquier usuario.
