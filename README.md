# Landing CINTRE — estado y cómo retomar

Sitio estático de un solo archivo (`index.html`). Sin build, sin dependencias, sin Node.

| | |
|---|---|
| **En vivo** | https://cintre.vercel.app |
| **Repo** | https://github.com/sekonsultingmx/landing-cintre |
| **Proyecto Vercel** | `cintre`, equipo Sekonsulting (Hobby) |
| **Carpeta local** | `C:\Users\Administrador\Desktop\Sekonsulting\landing-cintre` |
| **Rama** | `main` |

---

## Cómo hacer un cambio (flujo ya conectado)

El repo está conectado a Vercel: **cada push a `main` redespliega solo en ~40 segundos.**
La credencial de GitHub está guardada en el Administrador de credenciales de Windows, así que
los push no piden nada.

```powershell
$p="C:\Users\Administrador\Desktop\Sekonsulting\landing-cintre"
git -C $p add -A
git -C $p commit -m "Descripción del cambio"
git -C $p push
```

Después, verificar en el sitio publicado que el cambio esté ahí. Añadir `?v=algo` a la URL
evita leer una versión en caché.

**No hace falta navegador ni sesión de Vercel para editar y publicar.** El navegador solo sirve
para revisar visualmente el resultado, que es recomendable pero no obligatorio.

### Si algo sale mal

Vercel guarda todos los despliegues. En el panel del proyecto → *Deployments* → **Instant
Rollback** se regresa a cualquier versión anterior con un clic. En Git, `git revert <commit>`
deshace un cambio concreto conservando el historial.

### Para cambios grandes o que el cliente aún no aprueba

Trabajar en una rama: Vercel genera una **URL de preview** independiente, así se le puede enseñar
un borrador a CINTRE sin tocar lo que está en vivo.

```powershell
git -C $p checkout -b nombre-del-cambio
```

---

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Todo el sitio: HTML, CSS y JS en línea. Ilustraciones en SVG embebido. |
| `og.png` | Imagen de vista previa al compartir la liga (1200×630). |
| `vercel.json` | Headers de seguridad y `X-Robots-Tag: noindex`. |

La imagen `og.png` se genera con un script de PowerShell + .NET (GDI+), porque la máquina no tiene
Node ni Python. Si hay que regenerarla, el script debe guardarse **con BOM UTF-8** o PowerShell 5.1
destroza los acentos.

---

## `noindex`: por qué está y cuándo se quita

Mientras CINTRE no apruebe la propuesta, el sitio va con `noindex` en **dos capas**:

- `<meta name="robots" content="noindex, nofollow">` en `index.html`
- header `X-Robots-Tag` en `vercel.json`

La página lleva el nombre, dirección y equipo reales de un negocio que todavía no la autorizó. Sin
`noindex` competiría en buscadores con su identidad, como si fuera su sitio oficial. Sigue siendo
accesible por la liga directa, que es lo único que se necesita para enseñársela.

**Al aprobarse y migrar al dominio del cliente, quitar ambas.**

---

## PENDIENTES

### Solo CINTRE puede confirmarlos — bloquean el envío de la liga

- **Teléfono.** El DENUE registra `55 2614 3031`; un directorio externo lista `55 5516 9613`.
- **Correo.** Hoy aparece `fveayra05@yahoo.com.mx`, un dominio gratuito. Conviene uno propio.
- **Horarios.** No hay fuente pública; los mostrados son un supuesto.
- **Títulos del equipo.** Solo está confirmado el de la Dra. Fedra Irazoque Palazuelos. Los otros
  cinco nombres van sin honorífico a propósito, para no asignar grado ni género por suposición.

Están marcados con `data-verificar="..."` en el HTML y en el comentario del encabezado del archivo.

### Se pueden hacer sin esperar al cliente

- Conectar el formulario a un destino real. Hoy avisa honestamente que es demostración y remite al
  teléfono; **no simula envíos exitosos**.
- Sustituir los avatares de iniciales por fotos reales del equipo, si las proporcionan.
- Fotos del consultorio y del área de infusiones.

---

## Historial

```
2e64558  Corrige proporciones del mapa corporal y ajusta su encuadre
58be3b9  Agrega ilustraciones anatómicas: mapa corporal, comparación articular, anticuerpo
a00fb89  Agrega imagen de vista previa (og.png)
1d09399  Agrega metadatos Open Graph
cc95f7d  Propuesta inicial
```
