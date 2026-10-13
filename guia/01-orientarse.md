# 1️⃣ Orientarse: ¿dónde estoy?

⏱️ 20 min · [⬅️ Anterior](00-antes-de-empezar.md) · [Inicio](../README.md) · [Siguiente ➡️](02-crear.md)

## La idea

**Sistema operativo (SO).** Es el programa principal del ordenador: Windows, macOS o Linux. Gestiona el hardware, los programas, los usuarios y **los archivos**. Todo lo demás funciona encima de él.

### GUI frente a CLI

Hay dos formas de dar órdenes al sistema operativo:

| | GUI (interfaz gráfica) | CLI (interfaz de línea de comandos) |
|---|---|---|
| Cómo se usa | Ventanas, iconos, ratón | Texto escrito en una terminal |
| Ejemplo: ver tus descargas | Abrir el explorador y hacer doble clic en Descargas | `ls ~/Downloads` |
| Ejemplo: mover 300 PDF a una carpeta | Seleccionarlos a mano, arrastrar | `mv *.pdf facturas/` |
| Ejemplo: saber qué archivo ocupa más espacio | Ordenar columna por columna, carpeta a carpeta | Un comando |
| Ventaja | Intuitiva, visual, no hay que memorizar | Rápida, precisa, repetible y automatizable |
| Inconveniente | Lenta para tareas repetitivas | Hay que aprender los comandos |
| Dónde es imprescindible | Diseño, ofimática, uso diario | Servidores, programación, administración de sistemas, nube, automatización |

Las dos acceden **a los mismos archivos**. La CLI no es "más antigua" ni "para expertos". Es otra herramienta, y en muchos trabajos técnicos es la principal: la mayoría de servidores de internet no tienen interfaz gráfica.

**Terminal y shell.** La **terminal** es la ventana donde escribes. La **shell** es el programa que interpreta lo que escribes y se lo pasa al sistema operativo. Cada sistema trae la suya:

| Sistema | Shell por defecto |
|---|---|
| macOS | `zsh` |
| Linux | `bash` |
| Windows | `PowerShell` |

Casi todos los comandos de hoy son iguales en las tres. Cuando cambian, las tablas tienen una columna para cada sistema.

### Anatomía de un comando

```
ls   -a   Downloads
│    │    │
│    │    └── argumento: sobre qué actúa (una carpeta, un archivo...)
│    └── opción: cómo lo hace (empieza por - o --)
└── comando: qué hace (en realidad, el nombre de un programa)
```

Cada comando es **un programa** instalado en tu ordenador. Cuando escribes `ls`, la shell busca un programa llamado `ls` y lo ejecuta. Lo verás a fondo en el [módulo 5](05-ejecutar.md).

**El sistema de archivos es un árbol.** Hay una carpeta raíz y de ella salen todas las demás. La terminal siempre está "dentro" de una carpeta: tu **posición**. Al abrirla, estás en tu **carpeta personal**.

```
/  (Mac/Linux)   ·   C:\  (Windows)          ← la raíz
└── Users  (o home)
    └── ana                                  ← tu carpeta personal  =  ~
        ├── Desktop   (Escritorio)
        ├── Documents (Documentos)
        ├── Downloads (Descargas)
        └── taller                           ← aquí trabajaremos hoy
```

## Los comandos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Saber quién soy | `whoami` | `whoami` |
| Saber **dónde estoy** | `pwd` | `pwd` |
| Ver qué hay aquí | `ls` | `ls` |
| Ver también lo oculto | `ls -a` | `ls -Force` |
| Ver con detalle (tamaño, fecha) | `ls -l` | `ls` (ya lo muestra) |
| Entrar en una carpeta | `cd Documents` | `cd Documents` |
| Subir a la carpeta de arriba | `cd ..` | `cd ..` |
| Ir a mi carpeta personal | `cd ~` (o solo `cd`) | `cd ~` |
| Volver a la carpeta anterior | `cd -` | `cd -` (solo PowerShell 7) |
| Ir a la raíz | `cd /` | `cd \` |
| Ver qué sistema tengo | Mac: `sw_vers` · Linux: `cat /etc/os-release` | `Get-ComputerInfo -Property OsName` |
| Limpiar la pantalla | `clear` | `clear` |

**Símbolos que vas a usar siempre:**

| Símbolo | Significa |
|---|---|
| `~` | Tu carpeta personal |
| `.` | La carpeta donde estoy ahora |
| `..` | La carpeta de arriba (la "madre") |
| `/` | Separa carpetas en una ruta: `Documents/trabajo`. Windows acepta `/` y `\` |

## Rutas absolutas y relativas

Una **ruta** es la dirección de una carpeta o archivo.

- **Absoluta**: desde la raíz. Funciona estés donde estés. `/Users/ana/Documents` o `C:\Users\ana\Documents`.
- **Relativa**: desde donde estás. `Documents` solo funciona si estás en tu carpeta personal.

Es la diferencia entre una dirección postal completa (absoluta) y una indicación como "la segunda puerta a la derecha" (relativa).

---

## 🧪 Pruébalo

Escribe cada línea y pulsa Enter. Compara con lo que deberías ver.

**1. ¿Dónde estoy?**
```
pwd
```
✅ Algo como `/Users/orwell`, `/home/orwell` o `C:\Users\orwell`. Es tu carpeta personal.

**2. ¿Qué hay aquí?**
```
ls
```
✅ Las carpetas de siempre: `Desktop`, `Documents`, `Downloads`... Son las mismas que ves en el explorador de archivos.

**3. Entra en Descargas y mira qué hay.**
```
cd Downloads
ls
```
✅ Tus descargas. En Linux en español la carpeta se llama `Descargas`: usa `cd Descargas`. En Mac, si aparece un aviso de permisos, pulsa **Permitir**.

**4. Vuelve arriba y comprueba.**
```
cd ..
pwd
```
✅ Otra vez en tu carpeta personal.

**5. Usa Tab.** Escribe `cd Doc` y pulsa **Tab** antes de Enter.
✅ Se completa solo: `cd Documents` (en Linux en español, escribe `cd Doc` y verás `Documentos`). Pulsa Enter. Si hay varias opciones, pulsa Tab dos veces y te las muestra.

**6. Ve a la raíz y vuelve a tu carpeta personal.**
```
cd /
ls
cd ~
pwd
```
✅ En la raíz ves carpetas del sistema. Con `cd ~` vuelves a tu carpeta personal desde cualquier sitio.

**7. Archivos ocultos.** En tu carpeta personal:
```
ls -a
```
En Windows: `ls -Force`.
✅ Aparecen archivos que empiezan por punto (`.zshrc`, `.config`...). Son configuraciones. Están ocultos para que no los toques sin querer.

**8. Terminal y explorador.** Abre el explorador de archivos **en la carpeta donde estás**:

| Mac | Linux | Windows |
|---|---|---|
| `open .` | `xdg-open .` | `explorer .` |

✅ Se abre una ventana con las mismas carpetas que lista `ls`. **La terminal y el explorador son dos formas de ver lo mismo.**

---

## ⚠️ Errores típicos

| Ves esto | Qué pasa | Qué hacer |
|---|---|---|
| `no such file or directory` · `No se encuentra la ruta` | Esa carpeta no está **donde estás tú**, o  está mal escrita | `pwd` para saber dónde estás, `ls` para ver qué hay. Usa Tab |
| `command not found` · `no se reconoce como nombre de un cmdlet` | El comando está mal escrito | Flecha ↑, corrige y Enter |
| `cd documents` no funciona en Mac | Las mayúsculas importan | `cd Documents` |
| Una carpeta tiene espacios: `cd Mis Documentos` falla | El espacio separa palabras | Comillas: `cd "Mis Documentos"`. O escribe `cd Mis` y pulsa Tab |



## 🔥 Preguntas

1. ¿Qué diferencia hay entre `cd ..` y `cd ../..`? Pruébalo.
2. Mac/Linux: compara `ls -l` y `ls -la`. ¿Qué significan las columnas? Pista: permisos, propietario, tamaño, fecha.
3. ¿Qué devuelve `echo $HOME`? En Windows: `echo $HOME` también. ¿Y `echo $SHELL` en Mac/Linux?
4. Mira tu historial: `history`. ¿Cuántos comandos llevas?


---

[⬅️ Anterior](00-antes-de-empezar.md) · [Siguiente: Crear ➡️](02-crear.md)
