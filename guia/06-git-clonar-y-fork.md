# 6️⃣ Git: tu propia copia del taller

⏱️ 25 min · 👥 Todo el grupo · [⬅️ Anterior](05-ejecutar.md) · [Inicio](../README.md)

## La idea

**Git** guarda el historial de una carpeta. Cada vez que llegas a un punto que quieres conservar, haces un **commit**: una "foto" de tus archivos con un mensaje que explica qué cambiaste.

**GitHub** es la web donde se guardan esas carpetas. Se llaman **repositorios**.

Al terminar este módulo tendrás **tu propia copia del taller**, en GitHub y en tu ordenador. Ahí harás las prácticas y subirás tus cambios.

```
  GitHub: repositorio del taller
              │
              │  1. FORK  (botón en GitHub)
              ▼
  GitHub: TU copia  →  github.com/tu-usuario/taller-terminal
              │                    ▲
              │  2. CLONE          │  4. PUSH (subir cambios)
              ▼                    │
  Tu ordenador: ~/taller/taller-terminal
              │
              └─ 3. trabajas: creas, editas, borras archivos
```

| Palabra | Qué es |
|---|---|
| **Fork** | Hacer una copia de un repositorio ajeno **en tu cuenta de GitHub** |
| **Clone** | Descargar un repositorio de GitHub **a tu ordenador** |
| **Commit** | Guardar una "foto" de tus cambios, con un mensaje |
| **Push** | Subir tus commits a GitHub |

---

## Paso 1 — Instalar Git

Comprueba si ya lo tienes:
```
git --version
```
Si aparece `git version 2.xx`, salta a "Preséntate a Git".

| Sistema | Instalación |
|---|---|
| **Windows** | `winget install --id Git.Git -e --source winget` → acepta lo que pida → **cierra PowerShell y ábrelo de nuevo**. Si `winget` no se reconoce, descarga el instalador de [git-scm.com/download/win](https://git-scm.com/download/win) y deja todas las opciones por defecto |
| **Mac** | `xcode-select --install` → en la ventana que aparece, pulsa **Instalar** (tarda unos minutos) |
| **Linux** | `sudo apt update` y después `sudo apt install git -y` |

✅ `git --version` muestra la versión.

**Preséntate a Git.** Solo se hace una vez. Usa el mismo correo que en GitHub:
```
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@ejemplo.com"
```
✅ No dice nada. Silencio = éxito.

---

## Paso 2 — Fork: tu copia en GitHub

1. Abre el repositorio del taller en el navegador.
2. Arriba a la derecha, pulsa **Fork**.
3. Pulsa **Create fork**.

✅ La dirección del navegador ahora es `github.com/TU-USUARIO/taller-terminal`. Esta copia es **tuya**: puedes cambiar lo que quieras sin afectar al original.

---

## Paso 3 — Clone: tu copia en tu ordenador

1. En **tu fork**, pulsa el botón verde **Code** → pestaña **HTTPS** → icono de copiar 📋.
2. En la terminal:
   ```
   cd ~/taller
   git clone https://github.com/TU-USUARIO/taller-terminal.git
   ```
   Pega la dirección que has copiado: **Cmd + V** en Mac, **Ctrl + Shift + V** en Linux, **clic derecho** o **Ctrl + V** en Windows.
3. Entra y mira lo que has descargado:
   ```
   cd taller-terminal
   ls
   ```

✅ Ves `README.md`, `chuleta.md`, `guia`, `practica`... Son los mismos archivos que en GitHub, ahora en tu ordenador.

---

## Paso 4 — El ciclo de Git: status, add, commit, push

Estos **cuatro comandos** son el 90 % del uso diario de Git. Los vas a repetir siempre en el mismo orden.

| # | Comando | Qué hace | Pregunta que responde |
|---|---|---|---|
| 1 | `git status` | Muestra qué ha cambiado | ¿Qué he tocado? |
| 2 | `git add .` | Prepara **todos** los cambios para guardarlos | ¿Qué quiero guardar? |
| 3 | `git commit -m "mensaje"` | Guarda la foto con un mensaje | ¿Qué he hecho? |
| 4 | `git push` | Sube los commits a tu GitHub | ¿Lo comparto? |

💡 **`git status` es tu `pwd` de Git.** Si no sabes en qué punto estás, escríbelo. Puedes usarlo todas las veces que quieras: no cambia nada.

### 🧪 Pruébalo: tu primer commit

Desde `~/taller/taller-terminal`:

**1. Mira el estado.**
```
git status
```
✅ `nothing to commit, working tree clean`. Todo está igual que en GitHub.

**2. Haz un cambio.** Crea tu archivo de notas:

Mac / Linux:
```
echo "# Mis notas del taller" > mis-notas.md
echo "Comando favorito: ls" >> mis-notas.md
```
Windows:
```
Set-Content mis-notas.md "# Mis notas del taller"
Add-Content mis-notas.md "Comando favorito: ls"
```

> [!IMPORTANT]
> **Windows:** para archivos que vas a subir a GitHub, usa `Set-Content` (crear) y `Add-Content` (añadir) en lugar de `>` y `>>`. En PowerShell 5, `>` guarda el texto en un formato (UTF-16) que GitHub no muestra bien. También puedes escribir el archivo con `notepad mis-notas.md`.

**3. Vuelve a mirar el estado.**
```
git status
```
✅ `mis-notas.md` aparece en **rojo**, bajo *Untracked files*. Git ha visto un archivo nuevo, pero todavía no lo guarda.

**4. Prepara el cambio.**
```
git add .
git status
```
✅ Ahora `mis-notas.md` está en **verde**, bajo *Changes to be committed*. Está listo para guardarse.

**5. Guarda la foto.**
```
git commit -m "Añado mis notas del taller"
```
✅ Aparece algo como `1 file changed, 2 insertions(+)`.

**6. Súbelo a GitHub.**
```
git push
```
La primera vez, GitHub te pedirá identificarte. Mira el apartado siguiente.

✅ Recarga **tu fork** en el navegador: `mis-notas.md` está ahí. 🎉

### La primera vez que haces push: identificarte

GitHub necesita saber que eres tú.

**Windows.** Se abre una ventana para iniciar sesión. Pulsa **Sign in with your browser**, acepta en el navegador y vuelve a la terminal. No tendrás que repetirlo.

**Mac y Linux.** La terminal pide `Username` y `Password`. **No es la contraseña de GitHub**: GitHub ya no la acepta desde la terminal. Necesitas un **token**, una clave larga que haces una sola vez.

1. En GitHub: tu avatar → **Settings** → abajo del todo, **Developer settings** → **Personal access tokens** → **Tokens (classic)** → **Generate new token (classic)**.
2. **Note:** `taller`. **Expiration:** 90 days. Marca la casilla **repo**.
3. Pulsa **Generate token** y **cópialo ya**. GitHub no te lo vuelve a enseñar.
4. En la terminal: en `Username` escribe tu usuario de GitHub. En `Password`, pega el token. No verás nada al pegarlo: es normal. Pulsa Enter.

Para que no te lo pida cada vez:
- **Mac:** se guarda solo en el Llavero.
- **Linux:** antes del push, ejecuta `git config --global credential.helper store`.

---

## 🎯 Reto: repite el ciclo tú sola/o

👥 Individual · ⏱️ 5 min

Haz **tres commits más**, cada uno con su `status`, `add`, `commit` y `push`:

1. Añade a `mis-notas.md` tres comandos que hayas aprendido hoy. Mac y Linux: `>>`. Windows: `Add-Content`.
2. Crea una carpeta `mis-practicas` con un archivo dentro. Git no sube carpetas vacías: tiene que haber un archivo.
3. Borra un archivo que hayas creado tú y comprueba qué dice `git status`.

✅ **Comprueba:** en tu fork en GitHub aparecen los cambios. Pulsa en el reloj 🕒 **Commits** para ver tu historial: cada commit con tu mensaje.

<details>
<summary>💡 Pista: el ciclo, siempre igual</summary>

```
git status
git add .
git commit -m "Explico qué he cambiado"
git push
```
</details>

**Un buen mensaje de commit** dice qué has hecho, en una línea: `Añado tres comandos a mis notas`. Mensajes como `cambios`, `asdf` o `final` no sirven a nadie, tampoco a ti dentro de un mes.

---

## ⚠️ Errores típicos

| Ves esto | Qué pasa | Qué hacer |
|---|---|---|
| `git: command not found` / `no se reconoce` | Git no está instalado, o la terminal no se ha reiniciado tras instalarlo | Cierra la terminal y ábrela de nuevo |
| `fatal: not a git repository` | No estás dentro de la carpeta del repositorio | `cd ~/taller/taller-terminal` |
| `nothing to commit, working tree clean` | No has cambiado nada, o ya lo has guardado | Normal. Haz un cambio primero |
| `nothing added to commit but untracked files present` | Te has saltado el `git add .` | `git add .` y repite el commit |
| `Please tell me who you are` | No has hecho el `git config` del paso 1 | Ejecuta los dos `git config` |
| `Authentication failed` / `Invalid username or token` | Has usado la contraseña de GitHub o el token está mal copiado | Genera un token nuevo y pégalo con cuidado |
| `Permission denied` o `403` al hacer push | Has clonado el repositorio del taller en vez de **tu fork** | Comprueba que la dirección del clone tiene **tu** usuario |
| Se abre un editor raro (Vim) y no sabes salir | Has escrito `git commit` sin `-m` | Escribe `:q!` y Enter. Repite con `-m "mensaje"` |
| `destination path already exists` | Ya lo clonaste antes en esta carpeta | Ya lo tienes: `cd taller-terminal` |

---

## 🏆 Reto final: escape room

En tu copia está la carpeta `practica/escape-room`. Se resuelve con los comandos de los módulos 1 a 4.

```
cd ~/taller/taller-terminal/practica/escape-room
cat LEEME.txt
```

Para crear `clave.txt` en Windows, usa `Set-Content` en lugar de `>`, por el mismo motivo que antes.

Cuando lo resuelvas, **sube tu solución** con el ciclo de Git: `git status`, `git add .`, `git commit -m "Resuelvo el escape room"`, `git push`.

---

## 🔥 Modo experto

Cuando el ciclo básico te salga sin mirar:

| Comando | Para qué |
|---|---|
| `git log --oneline` | Ver el historial en la terminal. Sal con `q` |
| `git diff` | Ver **exactamente** qué líneas has cambiado, antes del `add` |
| `git restore archivo` | Deshacer los cambios de un archivo que aún no has guardado en un commit |
| `git pull` | Bajar a tu ordenador cambios hechos en GitHub (por ejemplo, si editas desde la web) |
| `git remote -v` | Ver a qué repositorio de GitHub está conectada tu carpeta |

**Propón un cambio al repositorio original (pull request):**
1. Añade tu usuario al final de `participantes.md`. Mac y Linux: `echo "- @tu-usuario" >> participantes.md`. Windows: `Add-Content participantes.md "- @tu-usuario"`.
2. Ciclo completo: `status`, `add`, `commit`, `push`.
3. En tu fork en GitHub aparece *"This branch is 1 commit ahead"*. Pulsa **Contribute** → **Open pull request** → **Create pull request**.

✅ Si se acepta, tu nombre aparecerá en el repositorio del taller. Así se colabora en cualquier proyecto de código abierto.

**Recibir las novedades del taller en tu fork:** en tu fork en GitHub, pulsa **Sync fork** → **Update branch**. Después, en la terminal, `git pull`.

---

[⬅️ Anterior](05-ejecutar.md) · [Inicio](../README.md) · [Chuleta](../chuleta.md)
