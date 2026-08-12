# Landing CINTRE — despliegue en Vercel

Sitio estático de un solo archivo (`index.html`). Sin build, sin dependencias.

## Estado

Propuesta comercial de Sekonsulting, **no aprobada aún por el cliente**. Por eso el sitio va
con `noindex` en dos capas (meta tag en el HTML y header `X-Robots-Tag` en `vercel.json`):
no debe indexarse ni aparecer en buscadores como si fuera el sitio oficial de CINTRE.

Al aprobarse y migrar al dominio del cliente, quitar ambas.

---

## Opción A — Arrastrar y soltar (la más rápida, cero instalaciones)

1. Entrar a https://vercel.com/new con la cuenta de Sekonsulting.
2. Buscar la opción de desplegar una carpeta / *deploy from template or folder*.
3. Arrastrar la carpeta `landing-cintre` completa.
4. Vercel detecta sitio estático y publica en una URL `*.vercel.app`.

Sirve para enseñarle la propuesta al cliente hoy mismo.

---

## Opción B — Git + integración de GitHub (recomendada para iterar)

Esta carpeta ya es un repositorio git con un commit inicial.

```bash
git remote add origin https://github.com/<cuenta-sekonsulting>/landing-cintre.git
git push -u origin main
```

Después, en https://vercel.com/new → *Import Git Repository* → seleccionar el repo.
A partir de ahí cada `git push` genera un despliegue automático, con URL de preview por rama.

---

## Opción C — Vercel CLI

Requiere Node.js, que **no está instalado en esta máquina**. Instalar primero desde
https://nodejs.org (versión LTS), y luego:

```bash
npm i -g vercel
```

```bash
vercel login
```

```bash
vercel deploy --prod
```

---

## Sobre el MCP de Vercel

`https://mcp.vercel.com` sirve para **consultar y administrar** proyectos, despliegues, logs
y analíticas — no para subir archivos locales ni crear un despliegue desde cero. El despliegue
inicial tiene que salir por alguna de las tres opciones de arriba.

Ya quedó declarado en `../.mcp.json`. Falta autorizarlo por OAuth con la cuenta de Sekonsulting.

---

## Pendientes antes de mandarle la liga al cliente

Ver el bloque de comentarios al inicio de `index.html`. En resumen:

- Confirmar teléfono (55 2614 3031 vs 55 5516 9613).
- Definir correo de contacto en dominio propio.
- Confirmar horarios de atención.
- Confirmar títulos y grados del equipo médico.
- Conectar el formulario a un destino real (hoy solo avisa que es demostración).
