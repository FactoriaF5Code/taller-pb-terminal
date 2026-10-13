# 2️⃣ Crear carpetas y archivos

⏱️ 15 min · [⬅️ Anterior](01-orientarse.md) · [Inicio](../README.md) · [Siguiente ➡️](03-copiar-mover-borrar.md)

## La idea

Hasta ahora has **mirado**. Ahora vas a **construir**. Todo lo que crees en la terminal aparece también en el explorador de archivos, porque es el mismo sitio.

Para crear, mover y borrar trabajamos siempre dentro de una carpeta de prácticas: **`~/taller`**. Para mirar y buscar usaremos tus carpetas reales, pero sin modificarlas.

> [!TIP]
> **Reglas para los nombres:** sin espacios (usa `-`), sin tildes ni ñ, en minúsculas. `mi-proyecto`, no `Mi Proyecto`. La terminal te lo agradecerá.

## Los comandos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Crear una carpeta | `mkdir fotos` | `mkdir fotos` |
| Crear varias a la vez | `mkdir fotos musica videos` | `mkdir fotos, musica, videos` |
| Crear carpetas anidadas | `mkdir -p a/b/c` | `mkdir a/b/c` |
| Crear un archivo vacío | `touch nota.txt` | `ni nota.txt` |
| Crear varios archivos vacíos | `touch a.txt b.txt` | `ni a.txt, b.txt` |
| Crear un archivo **con texto** | `echo "hola" > nota.txt` | `echo "hola" > nota.txt` |
| **Añadir** una línea al final | `echo "adios" >> nota.txt` | `echo "adios" >> nota.txt` |
| Ver el contenido | `cat nota.txt` | `cat nota.txt` |
| Editar un archivo en la terminal | `nano nota.txt` | `notepad nota.txt` (abre el Bloc de notas) |
| Abrir el archivo con su programa | Mac: `open nota.txt` · Linux: `xdg-open nota.txt` | `start nota.txt` |

**`>` frente a `>>`:**

| Símbolo | Qué hace | Ojo |
|---|---|---|
| `>` | Escribe en el archivo. Si existe, **sustituye todo** lo que tenía | Borra el contenido anterior sin avisar |
| `>>` | **Añade** al final, sin borrar | El seguro |

💡 `ni` es la abreviatura de `New-Item` en PowerShell. `touch` no existe en Windows.

💡 **Windows:** `mkdir` y `ni` muestran una pequeña tabla con lo que acaban de crear. Es normal: en PowerShell, a veces el éxito no es silencioso.

💡 **En `nano`:** guarda con **Ctrl + O** y Enter. Sal con **Ctrl + X**. Los atajos están abajo de la pantalla (`^` significa Ctrl).

---

## 🧪 Pruébalo

**1. Crea la carpeta del taller y entra.**
```
cd ~
mkdir taller
cd taller
pwd
```
✅ La ruta termina en `taller`. Será tu carpeta de trabajo toda la clase.

**2. Crea la estructura típica de un proyecto.** Casi cualquier proyecto digital (una web, un programa, un informe técnico) se organiza así: documentación, código e imágenes.

Mac / Linux:
```
mkdir mi-proyecto
cd mi-proyecto
mkdir docs src img
ls
```
Windows:
```
mkdir mi-proyecto
cd mi-proyecto
mkdir docs, src, img
ls
```
✅ Ves `docs`, `img` y `src`.

**3. Crea un archivo con texto.**
```
echo "# Mi proyecto" > README.md
cat README.md
```
✅ Se muestra `# Mi proyecto`. Acabas de crear un `README.md`, el mismo tipo de archivo que estás leyendo en GitHub.

**4. Añade líneas sin borrar las anteriores.**
```
echo "Proyecto creado desde la terminal." >> README.md
echo "Autoria: tu nombre" >> README.md
cat README.md
```
✅ Tres líneas, en orden.

**5. Comprueba el peligro de `>`.**
```
echo "Linea nueva" > README.md
cat README.md
```
✅ Solo queda una línea. **`>` ha sustituido todo el contenido.** Así se pierde un archivo de configuración o un registro en un segundo. Vuelve a escribir el README con `>` la primera línea y `>>` las siguientes.

**6. Crea archivos vacíos sin entrar en su carpeta.**

Mac / Linux: `touch src/index.html src/estilos.css docs/notas.txt`
Windows: `ni src/index.html, src/estilos.css, docs/notas.txt`

```
ls src
ls docs
```
✅ Los archivos están en su sitio. No has entrado en las carpetas: has usado **rutas relativas**.

**7. Edita un archivo.**

Mac / Linux: `nano docs/notas.txt`. Escribe dos líneas, guarda con **Ctrl + O**, Enter, y sal con **Ctrl + X**.
Windows: `notepad docs/notas.txt`. Escribe, guarda con **Ctrl + S** y cierra.

```
cat docs/notas.txt
```
✅ Se ve lo que has escrito, sin haber abierto el explorador.

**8. Carpetas anidadas de un golpe.**

Mac / Linux: `mkdir -p docs/2026/actas`
Windows: `mkdir docs/2026/actas`

✅ Comprueba con `cd docs/2026/actas` y `pwd`. Vuelve con `cd ~/taller/mi-proyecto`.

**9. Abre el resultado con la interfaz gráfica.** Desde `~/taller/mi-proyecto`:

| Mac | Linux | Windows |
|---|---|---|
| `open .` | `xdg-open .` | `explorer .` |

✅ Se abre el explorador con lo que has creado escribiendo. **CLI y GUI, los mismos archivos.**

---

## ⚠️ Errores típicos

| Ves esto | Qué pasa | Qué hacer |
|---|---|---|
| `File exists` · `Ya existe un elemento` | Esa carpeta ya existe | No pasa nada. Usa otro nombre o entra en ella |
| `touch` no se reconoce (Windows) | No existe en PowerShell | Usa `ni archivo.txt` |
| `mkdir a b c` crea una sola carpeta o da error (Windows) | PowerShell separa con comas | `mkdir a, b, c` |
| `dquote>` o `>>` y no vuelve el prompt | Has abierto unas comillas y no las has cerrado | **Ctrl + C** y vuelve a escribir |
| `event not found` (Mac/Linux) | Has puesto `!` entre comillas dobles | Usa comillas simples: `echo 'hola!'` |
| Se ha creado `mi` y `carpeta` en vez de `mi carpeta` | El espacio separa | Usa guion: `mi-carpeta` |

---

## 🎯 Reto: el arquitecto

👥 Individual · ⏱️ 7 min

Dentro de `~/taller`, construye **exactamente** esta estructura solo con la terminal:

```
taller/
└── proyecto-web/
    ├── LEEME.txt          → con dos líneas: "Proyecto web" y tu nombre
    ├── css/
    │   └── estilos.css    → vacío
    ├── img/
    └── paginas/
        ├── inicio.html    → vacío
        └── contacto.html  → vacío
```

✅ **Comprueba:**
- `cat ~/taller/proyecto-web/LEEME.txt` muestra las dos líneas.
- Ábrelo en el explorador y compara con el dibujo.
- Pega en el chat el número de comandos que has usado. ¿Quién lo ha hecho con menos?

<details>
<summary>💡 Solución (Mac / Linux)</summary>

```
cd ~/taller
mkdir -p proyecto-web/css proyecto-web/img proyecto-web/paginas
cd proyecto-web
echo "Proyecto web" > LEEME.txt
echo "Ana" >> LEEME.txt
touch css/estilos.css paginas/inicio.html paginas/contacto.html
cat LEEME.txt
```
</details>

<details>
<summary>💡 Solución (Windows)</summary>

```
cd ~/taller
mkdir proyecto-web/css, proyecto-web/img, proyecto-web/paginas
cd proyecto-web
echo "Proyecto web" > LEEME.txt
echo "Ana" >> LEEME.txt
ni css/estilos.css, paginas/inicio.html, paginas/contacto.html
cat LEEME.txt
```
</details>



---

[⬅️ Anterior](01-orientarse.md) · [Siguiente: Copiar, mover y borrar ➡️](03-copiar-mover-borrar.md)
