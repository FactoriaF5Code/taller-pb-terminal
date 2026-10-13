# 📄 Chuleta de la terminal

Referencia completa del taller. Sirve para seguir la clase y, sobre todo, para **repetir y practicar después**. Cada comando aparece en las dos versiones: **Mac / Linux** (`zsh`, `bash`) y **Windows** (`PowerShell`).

> [!NOTE]
> **Diferencias que conviene recordar:**
> - **Linux en español:** las carpetas se llaman `Descargas`, `Documentos` y `Escritorio`. En Mac y Windows, la terminal las muestra como `Downloads`, `Documents` y `Desktop`.
> - **Mac:** la primera vez que la terminal entra en Descargas o Documentos, pide permiso. Pulsa **Permitir**.
> - **Windows:** comprueba tu versión con `$PSVersionTable.PSVersion`. En PowerShell 5, `>` guarda los archivos en UTF-16: para archivos que vayan a GitHub, usa `Set-Content` y `Add-Content`.

**Índice:** [Conceptos](#1-conceptos-clave) · [Orientarse](#2-orientarse) · [Crear](#3-crear) · [Copiar, mover, borrar](#4-copiar-mover-y-borrar) · [Leer](#5-leer-archivos) · [Buscar](#6-buscar) · [Ejecutar y sistema](#7-ejecutar-programas-y-sistema) · [Git](#8-git) · [Símbolos](#9-símbolos-y-operadores) · [Teclado](#10-atajos-de-teclado) · [Recetas](#11-recetas-tareas-reales) · [Errores](#12-errores-frecuentes) · [Seguridad](#13-comandos-con-cuidado) · [Seguir aprendiendo](#14-seguir-aprendiendo)

---

## 1. Conceptos clave

| Concepto | Definición | Para recordarlo |
|---|---|---|
| **Sistema operativo** | Programa principal que gestiona hardware, programas, usuarios y archivos. Windows, macOS, Linux. | Todo lo demás funciona encima de él. |
| **GUI** | *Graphical User Interface*. Ventanas, iconos y ratón. | Intuitiva, pero lenta para tareas repetitivas. |
| **CLI** | *Command Line Interface*. Órdenes escritas. | Precisa, rápida, repetible y automatizable. |
| **Terminal** | La ventana donde escribes los comandos. | El "teclado y la pantalla". |
| **Shell** | El programa que interpreta lo que escribes: `zsh`, `bash`, `PowerShell`. | El "intérprete". |
| **Prompt** | La línea que espera tu orden. Acaba en `%`, `$` o `>`. | "Te escucho". |
| **Comando** | El nombre de un programa que la shell ejecuta. | `ls` es un programa, igual que el navegador, pero sin ventana. |
| **Opción** | Modifica cómo actúa un comando. Empieza por `-` o `--`. | `ls -a`: lista, **incluyendo lo oculto**. |
| **Argumento** | Sobre qué actúa el comando. | `cd Downloads`: entra **en Downloads**. |
| **Sistema de archivos** | Árbol de carpetas que parte de una raíz: `/` en Mac/Linux, `C:\` en Windows. | Cajas dentro de cajas. |
| **Directorio de trabajo** | La carpeta donde está la terminal ahora. | `pwd` te lo dice. |
| **Ruta absoluta** | Desde la raíz. Funciona desde cualquier sitio. | `/Users/ana/Documents` · `C:\Users\ana\Documents` |
| **Ruta relativa** | Desde donde estás. | `Documents`, `../Downloads` |
| **Carpeta personal** | Tu carpeta de usuario. Se escribe `~`. | Donde empieza la terminal. |
| **Archivo oculto** | En Mac/Linux, el que empieza por punto: `.zshrc`. | Suelen ser configuraciones. |
| **PATH** | Lista de carpetas donde la shell busca los programas. | Si un programa no está ahí: `command not found`. |
| **Alias** | Un nombre corto para otro comando. | En PowerShell, `ls` es un alias de `Get-ChildItem`. |
| **Proceso** | Un programa en ejecución. Tiene un número (PID). | Se puede cerrar con `kill` o `Stop-Process`. |
| **Script** | Archivo con una lista de comandos que se ejecutan de una vez. | `.sh` en Mac/Linux, `.ps1` en Windows. |
| **Gestor de paquetes** | Programa que instala otros programas desde la terminal. | `winget`, `brew`, `apt`. |
| **Git** | Programa que guarda el historial de cambios de una carpeta. | Vive en tu ordenador. |
| **GitHub** | Web que aloja repositorios de Git. | Vive en internet. |

---

## 2. Orientarse

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Saber quién soy | `whoami` | `whoami` |
| Saber dónde estoy | `pwd` | `pwd` |
| Ver qué hay aquí | `ls` | `ls` |
| Ver lo oculto | `ls -a` | `ls -Force` |
| Ver con detalle | `ls -l` · `ls -la` | `ls` |
| Ver tamaños legibles | `ls -lh` | `ls` |
| Ver el contenido de otra carpeta sin entrar | `ls ~/Downloads` | `ls ~/Downloads` |
| Entrar en una carpeta | `cd carpeta` | `cd carpeta` |
| Subir un nivel | `cd ..` | `cd ..` |
| Subir dos niveles | `cd ../..` | `cd ../..` |
| Ir a la carpeta personal | `cd` · `cd ~` | `cd ~` |
| Volver a la carpeta anterior | `cd -` | `cd -` (solo PowerShell 7) |
| Ir a la raíz | `cd /` | `cd \` |
| Carpeta con espacios | `cd "Mis Documentos"` | `cd "Mis Documentos"` |
| Abrir el explorador aquí | Mac: `open .` · Linux: `xdg-open .` | `explorer .` |
| Ver el sistema operativo | Mac: `sw_vers` · Linux: `cat /etc/os-release` | `Get-ComputerInfo -Property OsName` |
| Ver la shell que uso | `echo $SHELL` | `$PSVersionTable.PSVersion` |
| Limpiar la pantalla | `clear` · **Ctrl + L** | `clear` |
| Ver el historial de comandos | Linux: `history` · Mac: `history 1` | `history` |

---

## 3. Crear

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Crear una carpeta | `mkdir fotos` | `mkdir fotos` |
| Crear varias | `mkdir a b c` | `mkdir a, b, c` |
| Crear carpetas anidadas | `mkdir -p a/b/c` | `mkdir a/b/c` |
| Crear un archivo vacío | `touch nota.txt` | `ni nota.txt` |
| Crear varios archivos vacíos | `touch a.txt b.txt` | `ni a.txt, b.txt` |
| Crear una serie numerada | `touch nota-{1..10}.txt` | `1..10 \| % { ni "nota-$_.txt" }` |
| Escribir en un archivo (sustituye) | `echo "texto" > nota.txt` | `echo "texto" > nota.txt` · para GitHub: `Set-Content nota.txt "texto"` |
| Añadir al final | `echo "texto" >> nota.txt` | `echo "texto" >> nota.txt` · para GitHub: `Add-Content nota.txt "texto"` |
| Editar en la terminal | `nano nota.txt` | — |
| Editar con un programa gráfico | Mac: `open -e nota.txt` | `notepad nota.txt` |
| Abrir con el programa asociado | Mac: `open f` · Linux: `xdg-open f` | `start f` |

**En `nano`:** **Ctrl + O** y Enter guarda · **Ctrl + X** sale · **Ctrl + W** busca · **Ctrl + K** corta la línea.

---

## 4. Copiar, mover y borrar

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Copiar un archivo | `cp a.txt b.txt` | `cp a.txt b.txt` |
| Copiar a una carpeta | `cp a.txt carpeta/` | `cp a.txt carpeta/` |
| Copiar una carpeta entera | `cp -r origen destino` | `cp -r origen destino` |
| Copiar sin sobrescribir | `cp -n a.txt b.txt` | — |
| Mover | `mv a.txt carpeta/` | `mv a.txt carpeta/` |
| Renombrar | `mv viejo.txt nuevo.txt` | `mv viejo.txt nuevo.txt` |
| Mover preguntando si sobrescribe | `mv -i a.txt carpeta/` | `mv a.txt carpeta/ -Confirm` |
| Mover todos los de un tipo | `mv *.pdf facturas/` | `mv *.pdf facturas/` |
| Borrar un archivo | `rm a.txt` | `rm a.txt` |
| Borrar preguntando | `rm -i *.txt` | `rm *.txt -Confirm` |
| Simular un borrado | `ls *.tmp` (antes de `rm *.tmp`) | `rm *.tmp -WhatIf` |
| Borrar una carpeta vacía | `rmdir carpeta` | `rmdir carpeta` |
| Borrar una carpeta con todo | `rm -r carpeta` | `rm -r carpeta` |
| Borrar sin preguntar | `rm -rf carpeta` ⚠️ | `rm -r -Force carpeta` ⚠️ |
| Comprimir una carpeta | `zip -r copia.zip carpeta` | `Compress-Archive carpeta copia.zip` |
| Descomprimir | `unzip copia.zip` | `Expand-Archive copia.zip` |

---

## 5. Leer archivos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Ver un archivo | `cat f` | `cat f` |
| Ver con números de línea | `cat -n f` | `cat f \| % { "$($_.ReadCount): $_" }` |
| Primeras líneas | `head -n 10 f` | `cat f -Head 10` |
| Últimas líneas | `tail -n 10 f` | `cat f -Tail 10` |
| Seguir un archivo que crece (logs) | `tail -f f` | `cat f -Wait` |
| Leer página a página | `less f` (`q` para salir, `/` para buscar) | `cat f \| more` |
| Contar líneas | `wc -l f` | `(cat f).Count` |
| Contar palabras | `wc -w f` | `(cat f \| Measure-Object -Word).Words` |
| Comparar dos archivos | `diff a.txt b.txt` | `Compare-Object (cat a.txt) (cat b.txt)` |

---

## 6. Buscar

### Archivos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Por extensión en una carpeta | `ls *.pdf` | `ls *.pdf` |
| Por nombre, en subcarpetas | `find . -name "*.pdf"` | `ls -r -Filter *.pdf` |
| Sin distinguir mayúsculas | `find . -iname "*factura*"` | `ls -r -Filter *factura*` |
| Sin errores de permiso | `find ~ -name "x" 2>/dev/null` | `ls ~ -r -Filter x -ea 0` |
| Solo carpetas | `find . -type d` | `ls -r -Directory` |
| Solo archivos | `find . -type f` | `ls -r -File` |
| Más grandes de 100 MB | `find ~ -size +100M 2>/dev/null` | `ls ~ -r -File -ea 0 \| where Length -gt 100MB` |
| Modificados en los últimos 7 días | `find . -mtime -7` | `ls -r \| where LastWriteTime -gt (Get-Date).AddDays(-7)` |
| Ordenar por fecha | `ls -lt` | `ls \| sort LastWriteTime -Desc` |
| Ordenar por tamaño | `ls -lhS` | `ls \| sort Length -Desc` |
| Tamaño de una carpeta | `du -sh carpeta` | `(ls carpeta -r \| measure Length -Sum).Sum / 1MB` |
| Contar archivos | `ls \| wc -l` | `(ls).Count` |
| Dónde está un programa | `which git` | `Get-Command git` |

### Texto dentro de archivos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Líneas con una palabra | `grep "error" f` | `sls "error" f` |
| Sin distinguir mayúsculas | `grep -i "error" f` | `sls "error" f` |
| Distinguiendo mayúsculas | `grep "Error" f` | `sls "Error" f -CaseSensitive` |
| Con número de línea | `grep -n "error" f` | `sls "error" f` (ya lo muestra) |
| En toda una carpeta | `grep -rn "error" carpeta` | `ls carpeta -r \| sls "error"` |
| Solo nombres de archivo | `grep -rl "error" carpeta` | `ls carpeta -r \| sls "error" -List \| select Path` |
| Líneas que NO contienen | `grep -v "error" f` | `sls "error" f -NotMatch` |
| Contar coincidencias | `grep -c "error" f` | `(sls "error" f).Count` |

---

## 7. Ejecutar programas y sistema

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Versión de un programa | `git --version` | `git --version` |
| Ayuda de un comando | `man ls` · `ls --help` | `Get-Help ls` |
| Ver el PATH | `echo $PATH` | `$env:PATH -split ";"` |
| Abrir una web | Mac: `open URL` · Linux: `xdg-open URL` | `start URL` |
| Abrir una app | Mac: `open -a "Safari"` | `start chrome` · `calc` · `notepad` |
| Ejecutar un script | `bash script.sh` · `./script.sh` | `.\script.ps1` |
| Dar permiso de ejecución | `chmod +x script.sh` | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| Ejecutar como administrador | `sudo comando` | Abrir PowerShell con **Ejecutar como administrador** |
| Espacio en disco | `df -h` | `Get-PSDrive C` |
| Memoria | Mac: `vm_stat` · Linux: `free -h` | `Get-CimInstance Win32_OperatingSystem \| select FreePhysicalMemory` |
| Procesos | `top` · `ps aux` | `Get-Process` |
| Procesos que más consumen | `top -o cpu` (Mac) · `top` (Linux) | `Get-Process \| sort CPU -Desc \| select -First 10` |
| Buscar un proceso | `ps aux \| grep nombre` | `Get-Process *nombre*` |
| Cerrar un proceso | `kill PID` · `pkill nombre` | `Stop-Process -Id PID` · `Stop-Process -Name nombre` |
| Fecha y hora | `date` | `Get-Date` |
| Variable de entorno | `echo $HOME` · `echo $USER` | `$HOME` · `$env:USERNAME` |

### Red

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Comprobar conexión | `ping -c 4 github.com` | `ping github.com` |
| Mi IP local | Mac: `ipconfig getifaddr en0` · Linux: `hostname -I` | `ipconfig` |
| Mi IP pública | `curl ifconfig.me` | `curl.exe ifconfig.me` |
| Descargar un archivo | `curl -O URL` | `curl.exe -O URL` |
| Ver las cabeceras de una web | `curl -I https://github.com` | `curl.exe -I https://github.com` |
| Resolver un dominio | `nslookup github.com` | `nslookup github.com` |
| Ver la ruta hasta un servidor | `traceroute github.com` | `tracert github.com` |

### Instalar programas

| Sistema | Buscar | Instalar | Actualizar todo |
|---|---|---|---|
| Windows (`winget`) | `winget search vlc` | `winget install VideoLAN.VLC` | `winget upgrade --all` |
| macOS (`brew`) | `brew search wget` | `brew install wget` | `brew upgrade` |
| Ubuntu (`apt`) | `apt search tree` | `sudo apt install tree` | `sudo apt update && sudo apt upgrade` |

---

## 8. Git

| Quiero... | Comando (igual en todos los sistemas) |
|---|---|
| Comprobar si está instalado | `git --version` |
| Configurar nombre y correo (una vez) | `git config --global user.name "Nombre"` · `git config --global user.email "correo"` |
| Ver la configuración | `git config --global --list` |
| Descargar un repositorio | `git clone URL` |
| Descargarlo con otro nombre | `git clone URL nombre-carpeta` |
| Ver el estado | `git status` |
| Ver qué ha cambiado | `git diff` |
| Preparar cambios | `git add archivo` · `git add .` (todo) |
| Guardar un commit | `git commit -m "Mensaje claro"` |
| Ver el historial | `git log --oneline` |
| Subir commits a GitHub | `git push` |
| Bajar cambios de GitHub | `git pull` |
| Deshacer cambios no guardados | `git restore archivo` · `git restore .` |
| Borrar archivos nuevos no guardados | `git clean -fd` ⚠️ |
| Ver a qué repositorio apunta | `git remote -v` |
| Crear una rama y cambiarse a ella | `git switch -c nombre-rama` |
| Cambiar de rama | `git switch main` |

**Clonar frente a fork:**
- **Clonar** descarga un repositorio a tu ordenador. Si no es tuyo, no puedes subir cambios.
- **Fork** crea una copia del repositorio **en tu cuenta de GitHub**. Al clonar tu fork, sí puedes subir cambios a tu copia y proponerlos al original con una *pull request*.

**El ciclo de trabajo con Git** (lo que usarás el 90 % del tiempo):
```
git status                     →  ¿qué ha cambiado?
git add .                      →  prepara todos los cambios
git commit -m "Qué he hecho"   →  guarda una foto con un mensaje
git push                       →  súbela a tu GitHub
```

**Empezar con un repositorio ajeno:** Fork en GitHub → `git clone` de **tu** fork → ciclo de Git.

**Primer push en Mac o Linux:** la contraseña es un **token**, no la de GitHub. Se crea en Settings → Developer settings → Personal access tokens → Tokens (classic), con el permiso `repo`.

---

## 9. Símbolos y operadores

| Símbolo | Significado | Ejemplo |
|---|---|---|
| `~` | Carpeta personal | `cd ~/Downloads` |
| `.` | Carpeta actual | `open .` · `./script.sh` |
| `..` | Carpeta de arriba | `cd ..` |
| `/` | Separador de carpetas (Windows acepta también `\`) | `docs/2026/actas` |
| `*` | Cualquier texto | `*.pdf` · `factura-*` |
| `?` | Un carácter cualquiera | `informe-?.docx` |
| `{1..5}` | Serie (Mac/Linux) | `touch dia-{1..5}.txt` |
| `>` | Envía la salida a un archivo (sustituye) | `ls > lista.txt` |
| `>>` | Añade la salida al final de un archivo | `date >> lista.txt` |
| `\|` | Tubería: la salida de uno es la entrada del siguiente | `history \| grep cd` |
| `&&` | Ejecuta el segundo solo si el primero va bien | `mkdir x && cd x` |
| `&` | Ejecuta en segundo plano (Mac/Linux) | `gnome-calculator &` |
| `2>/dev/null` | Oculta los mensajes de error (Mac/Linux) | `find ~ -name x 2>/dev/null` |
| `$VARIABLE` | Valor de una variable | `echo $HOME` |
| `"..."` | Agrupa texto con espacios. Sustituye variables | `echo "Hola $USER"` |
| `'...'` | Agrupa texto tal cual. No sustituye variables | `echo 'Hola $USER'` |
| `#` | Comentario: la shell lo ignora (en scripts) | `# esto no se ejecuta` |

---

## 10. Atajos de teclado

| Tecla | Hace |
|---|---|
| **Tab** | Completa nombres de carpetas, archivos y comandos |
| **Tab Tab** | Muestra las opciones posibles |
| **↑ / ↓** | Recorre los comandos anteriores |
| **Ctrl + C** | Cancela el comando en curso |
| **Ctrl + L** | Limpia la pantalla |
| **Ctrl + A** / **Ctrl + E** | Va al principio / al final de la línea (Mac/Linux) |
| **Ctrl + U** | Borra la línea entera (Mac/Linux) |
| **Ctrl + R** | Busca en el historial mientras escribes |
| **Ctrl + D** | Cierra la terminal (Mac/Linux) |
| **q** | Sale de `less`, `more`, `man`, `top` y `git log` |
| **Ctrl + + / Ctrl + -** | Agranda o reduce la letra (Mac: Cmd) |
| **Copiar / pegar en la terminal** | Mac: Cmd + C / Cmd + V · Linux: Ctrl + Shift + C / Ctrl + Shift + V · Windows: Ctrl + C (con texto seleccionado) / Ctrl + V o clic derecho |

---

## 11. Recetas: tareas reales

**Encontrar un archivo del que solo recuerdo una parte del nombre**
```
Mac/Linux:  find ~ -iname "*contrato*" 2>/dev/null
Windows:    ls ~ -r -Filter *contrato* -ea 0 | select FullName
```

**Ver qué está llenando el disco**
```
Mac/Linux:  du -sh ~/* 2>/dev/null | sort -h | tail -n 10
Windows:    ls ~ -Directory | % { [pscustomobject]@{Carpeta=$_.Name; MB=[int]((ls $_.FullName -r -File -ea 0 | measure Length -Sum).Sum/1MB)} } | sort MB -Desc
```

**Ordenar la carpeta de Descargas por tipo**
```
Mac/Linux:  cd ~/Downloads && mkdir -p pdf imagenes && mv *.pdf pdf/ && mv *.jpg *.png imagenes/
Windows:    cd ~/Downloads; mkdir pdf, imagenes -ea 0; mv *.pdf pdf/; mv *.jpg imagenes/; mv *.png imagenes/
```

**Hacer una copia de seguridad con la fecha en el nombre**
```
Mac/Linux:  cp -r ~/Documents/proyecto ~/backups/proyecto-$(date +%Y-%m-%d)
Windows:    cp -r ~/Documents/proyecto ~/backups/proyecto-$(Get-Date -Format yyyy-MM-dd)
```

**Comprimir una carpeta para enviarla**
```
Mac/Linux:  zip -r proyecto.zip proyecto
Windows:    Compress-Archive proyecto proyecto.zip
```

**Buscar en qué archivo de un proyecto aparece un texto**
```
Mac/Linux:  grep -rn "texto" .
Windows:    ls -r -File | sls "texto"
```

**Guardar el listado de una carpeta en un archivo**
```
Mac/Linux:  ls -lh ~/Documents > ~/listado.txt
Windows:    ls ~/Documents > ~/listado.txt
```

**Cerrar un programa colgado**
```
Mac/Linux:  pkill -i nombre-del-programa
Windows:    Get-Process *nombre*   y después   Stop-Process -Name NombreExacto
```

**Comprobar si el problema es mi conexión o la web**
```
ping -c 4 8.8.8.8     (Windows: ping 8.8.8.8)     → responde: tengo internet
ping -c 4 github.com  (Windows: ping github.com)  → no responde: el problema es esa web o el DNS
```

**Repetir el último comando con permisos de administrador (Linux)**
```
sudo !!
```

---

## 12. Errores frecuentes

| Mensaje | Qué significa | Qué hacer |
|---|---|---|
| `command not found` · `no se reconoce como nombre de un cmdlet` | El comando está mal escrito, no está instalado o no está en el PATH | Revisa la escritura. Comprueba con `which` o `Get-Command`. Si acabas de instalarlo, reabre la terminal |
| `No such file or directory` · `No se encuentra la ruta` | El archivo o carpeta no existe donde lo buscas | `pwd` y `ls` para orientarte. Usa Tab |
| `Permission denied` · `Acceso denegado` | No tienes permiso sobre ese archivo o carpeta | Trabaja en tu carpeta personal. Si es necesario, `sudo` o PowerShell como administrador |
| `Is a directory` | Has usado un comando de archivos con una carpeta | `cd` para entrar. `cp -r` o `rm -r` para carpetas |
| `Not a directory` | Has usado `cd` con un archivo | `cat` para leerlo |
| `Directory not empty` | `rmdir` solo borra carpetas vacías | `rm -r` |
| `File exists` | Ya existe algo con ese nombre | Elige otro nombre |
| `dquote>` · `>>` sin prompt | Has abierto comillas sin cerrarlas | **Ctrl + C** |
| `event not found` | Has usado `!` entre comillas dobles (Mac/Linux) | Usa comillas simples |
| `Operation not permitted` (Mac) | La terminal no tiene permiso para esa carpeta | Ajustes del Sistema → Privacidad y seguridad → Archivos y carpetas → Terminal |
| GitHub muestra un archivo como binario o con caracteres raros | Se creó con `>` en PowerShell 5 (UTF-16) | Créalo con `Set-Content` o con `notepad` |
| `la ejecución de scripts está deshabilitada` (Windows) | Política de seguridad de PowerShell | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| `fatal: not a git repository` | No estás dentro de un repositorio | `cd` a la carpeta clonada |
| La terminal no responde | Un comando está esperando o en bucle | **Ctrl + C** |

---

## 13. Comandos con cuidado

La terminal hace exactamente lo que escribes, sin papelera y casi sin preguntar.

| Comando | Riesgo | Hábito seguro |
|---|---|---|
| `rm`, `rm -r` | Borra sin papelera | `pwd` y `ls` antes. Usa `rm -i` o `-WhatIf` |
| `rm -rf` · `rm -r -Force` | Borra todo sin preguntar | Nunca con `*`, `~` o `/` |
| `>` | Sustituye el contenido de un archivo | Usa `>>` si quieres añadir |
| `mv` | Sobrescribe si el destino existe | `mv -i` |
| `sudo` | Ejecuta con permisos de administrador | Solo si sabes qué hace el comando |
| `git clean -fd` | Borra archivos no guardados en Git | `git clean -n` primero, para ver qué borraría |
| Copiar comandos de internet | Pueden hacer cualquier cosa | Lee y entiende cada comando antes de pegarlo |

---

## 14. Seguir aprendiendo

| Recurso | Qué es | Idioma |
|---|---|---|
| [explainshell.com](https://explainshell.com) | Pega un comando y te explica cada parte | Inglés |
| [tldr pages](https://tldr.inbrowser.app) | Ejemplos prácticos de cada comando, sin la jerga del manual | Inglés |
| [Learn Git Branching](https://learngitbranching.js.org/?locale=es_ES) | Juego visual para aprender Git | Español |
| [Documentación de GitHub](https://docs.github.com/es) | Guía oficial | Español |
| [GitHub Skills](https://skills.github.com) | Cursos interactivos oficiales | Inglés |
| [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) | Juego de retos de terminal sobre un servidor real | Inglés |
| [Documentación de PowerShell](https://learn.microsoft.com/es-es/powershell/) | Guía oficial de Microsoft | Español |
| [Ubuntu: la línea de comandos para principiantes](https://ubuntu.com/tutorials/command-line-for-beginners) | Tutorial oficial | Inglés |

**Para practicar en casa:** repite los módulos de la [guía](guia/), haz tus prácticas en tu fork y súbelas con `status`, `add`, `commit` y `push`, y aplica una receta de la sección 11 a tu ordenador cada día.
