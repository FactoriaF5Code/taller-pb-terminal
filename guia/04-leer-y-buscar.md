# 4️⃣ Leer y buscar

⏱️ 15 min · [⬅️ Anterior](03-copiar-mover-borrar.md) · [Inicio](../README.md) · [Siguiente ➡️](05-ejecutar.md)

## La idea

"¿Dónde guardé aquel PDF?", "¿qué es lo que me está llenando el disco?", "¿qué archivo modifiqué ayer?". Con la GUI, estas preguntas llevan minutos de clics. Con la CLI, un comando.

En este módulo trabajas sobre **tus carpetas reales**, pero **solo para leer**. Ningún comando de esta página modifica nada.

> [!NOTE]
> - **Linux en español:** cambia `Downloads` por `Descargas` y `Documents` por `Documentos` en todos los comandos.
> - **Windows con OneDrive:** si `ls ~/Documents` sale vacío, tus documentos están en OneDrive. Usa `ls ~/OneDrive` para encontrarlos.

## Los comandos

### Leer archivos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Ver un archivo entero | `cat archivo` | `cat archivo` |
| Ver las primeras líneas | `head -n 5 archivo` | `cat archivo -Head 5` |
| Ver las últimas líneas | `tail -n 5 archivo` | `cat archivo -Tail 5` |
| Leer un archivo largo página a página | `less archivo` (sal con `q`) | `cat archivo \| more` (sal con `q`) |
| Contar líneas | `wc -l archivo` | `(cat archivo).Count` |

### Buscar archivos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Archivos de un tipo en una carpeta | `ls ~/Downloads/*.pdf` | `ls ~/Downloads/*.pdf` |
| Buscar por nombre en todas las subcarpetas | `find ~/Documents -name "*.pdf"` | `ls ~/Documents -r -Filter *.pdf` |
| Buscar por parte del nombre, sin importar mayúsculas | `find ~ -iname "*factura*"` | `ls ~ -r -Filter *factura* -ea 0` |
| Ordenar por fecha (lo más reciente primero) | `ls -lt` | `ls \| sort LastWriteTime -Desc` |
| Ordenar por tamaño (lo más grande primero) | `ls -lhS` | `ls \| sort Length -Desc` |
| Modificados en los últimos 7 días | `find ~/Documents -mtime -7` | `ls ~/Documents -r \| where LastWriteTime -gt (Get-Date).AddDays(-7)` |
| Cuánto ocupa una carpeta | `du -sh ~/Downloads` | `"{0:N0} MB" -f ((ls ~/Downloads -r \| measure Length -Sum).Sum / 1MB)` |
| Contar cuántos archivos hay | `ls ~/Downloads \| wc -l` | `(ls ~/Downloads).Count` |

### Buscar texto dentro de archivos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Líneas que contienen una palabra | `grep "palabra" archivo` | `sls "palabra" archivo` |
| Sin distinguir mayúsculas | `grep -i "palabra" archivo` | `sls "palabra" archivo` (ya lo hace) |
| En todos los archivos de una carpeta | `grep -rn "palabra" carpeta` | `ls carpeta -r \| sls "palabra"` |
| Solo los nombres de archivo que la contienen | `grep -rl "palabra" carpeta` | `ls carpeta -r \| sls "palabra" -List \| select Path` |

💡 `sls` es la abreviatura de `Select-String`, el `grep` de PowerShell. `-ea 0` significa "no muestres errores de carpetas sin permiso".

### Encadenar y guardar resultados

| Símbolo | Qué hace | Ejemplo |
|---|---|---|
| `\|` (tubería) | La salida de un comando se convierte en la entrada del siguiente | `history \| grep mkdir` |
| `>` | Guarda la salida en un archivo, en vez de mostrarla | `ls ~/Downloads > ~/taller/descargas.txt` |
| `>>` | La añade al final de un archivo | `date >> ~/taller/descargas.txt` |

La tubería es la idea más potente de la CLI: **comandos pequeños que se combinan**. Con la GUI no hay equivalente.

---

## 🧪 Pruébalo

**1. Lee un archivo de configuración real del sistema.** Todos los ordenadores tienen un archivo `hosts` que traduce nombres a direcciones IP.

Mac / Linux:
```
cat /etc/hosts
```
Windows:
```
cat C:\Windows\System32\drivers\etc\hosts
```
✅ Unas pocas líneas con `localhost` y `127.0.0.1`. Las que empiezan por `#` son comentarios.

**2. Busca una palabra dentro de ese archivo.**

Mac / Linux: `grep localhost /etc/hosts`
Windows: `sls localhost C:\Windows\System32\drivers\etc\hosts`

✅ Solo aparecen las líneas que contienen `localhost`.

**3. ¿Cuántos archivos tienes en Descargas?**

Mac / Linux: `ls ~/Downloads | wc -l`
Windows: `(ls ~/Downloads).Count`

✅ Un número. Probablemente más alto de lo que pensabas.

**4. ¿Qué es lo último que has descargado?**

Mac / Linux: `ls -lt ~/Downloads | head -n 5`
Windows: `ls ~/Downloads | sort LastWriteTime -Desc | select -First 5`

✅ Los 5 archivos más recientes, el primero arriba.

**5. ¿Qué es lo que más ocupa en Descargas?**

Mac / Linux: `ls -lhS ~/Downloads | head -n 5`
Windows: `ls ~/Downloads | sort Length -Desc | select -First 5 Name, Length`

✅ Los 5 más pesados. En Mac/Linux, `-h` muestra los tamaños en K, M, G. En Windows, `Length` está en bytes.

**6. Encuentra todos tus PDF, estén donde estén.**

Mac / Linux: `find ~ -iname "*.pdf" 2>/dev/null | head -n 20`
Windows: `ls ~ -r -Filter *.pdf -ea 0 | select -First 20 FullName`

✅ Las rutas completas de tus PDF. `2>/dev/null` (Mac/Linux) oculta los avisos de carpetas sin permiso. Puede tardar unos segundos.

**7. Busca entre los comandos que has usado hoy.**

Linux: `history | grep mkdir`
Mac: `history 1 | grep mkdir`
Windows: `history | sls mkdir`

✅ Solo los comandos `mkdir` que has escrito. Acabas de usar una **tubería**.
En Mac, `history` a secas solo muestra los últimos 16 comandos. Con `history 1` muestra todos desde el primero.

**8. Guarda un resultado en un archivo.**

Mac / Linux: `ls -lt ~/Downloads > ~/taller/listado-descargas.txt`
Windows: `ls ~/Downloads | sort LastWriteTime -Desc > ~/taller/listado-descargas.txt`

```
head ~/taller/listado-descargas.txt
```
En Windows: `cat ~/taller/listado-descargas.txt -Head 10`.
✅ El listado está guardado en un archivo, listo para enviarlo o compararlo otro día.

---

## ⚠️ Errores típicos

| Ves esto | Qué pasa | Qué hacer |
|---|---|---|
| Muchas líneas de `Permission denied` | `find` entra en carpetas del sistema sin permiso | Añade `2>/dev/null` al final |
| Se llena la pantalla y no para | El resultado es enorme | **Ctrl + C**. Añade `\| head` o `\| more` al final |
| `less` o `more` no te deja escribir | Estás dentro del visor | Pulsa `q` para salir |
| `grep` no encuentra nada | Mayúsculas distintas, o la palabra no está | Prueba con `grep -i` |
| `head` no se reconoce (Windows) | No existe en PowerShell | `cat archivo -Head 5` |
| `find` tarda mucho | Estás buscando en todo el disco | Busca en una carpeta concreta, no en `~` o `/` |

---

## 🎯 Reto: auditoría de tu propio ordenador

👥 Individual · ⏱️ 8 min

Responde con comandos. Pega en el chat de Zoom **solo los números**, nunca nombres de archivos personales.

1. ¿Cuántos archivos hay en tu carpeta de Descargas?
2. ¿Cuántos PDF tienes en Descargas?
3. ¿Cuánto ocupa tu carpeta de Descargas en total?
4. ¿Cuál es el archivo más grande de Descargas? (Míralo, no lo compartas.)
5. ¿Cuántos archivos has modificado en Documentos en los últimos 7 días?
6. ¿Cuántas veces has usado `cd` hoy? Pista: `history` (en Mac, `history 1`) y una tubería.





---

[⬅️ Anterior](03-copiar-mover-borrar.md) · [Siguiente: Ejecutar programas ➡️](05-ejecutar.md)
