# 5️⃣ Ejecutar programas desde la terminal

⏱️ 20 min · [⬅️ Anterior](04-leer-y-buscar.md) · [Inicio](../README.md) · [Siguiente ➡️](06-git-clonar-y-fork.md)

## La idea

**Cada comando es un programa.** `ls`, `ping` o `git` son programas instalados en tu ordenador, igual que el navegador. La diferencia es que no tienen ventana: reciben texto y devuelven texto.

**¿Cómo sabe la shell dónde está cada programa?** Por el **PATH**: una lista de carpetas donde la shell busca los programas cuando escribes su nombre. Si un programa no está en ninguna de esas carpetas, aparece el error `command not found`. Es el error más común al instalar herramientas nuevas.

**Desde la terminal puedes:**
- Abrir programas gráficos y páginas web.
- Consultar el estado del sistema: disco, red, procesos.
- Cerrar un programa que se ha colgado.
- Instalar programas con un **gestor de paquetes**.
- Ejecutar **scripts**: archivos con una lista de comandos que se ejecutan de una vez.

## Los comandos

### Programas y PATH

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Saber dónde está un programa | `which ls` | `Get-Command ls` |
| Ver las carpetas del PATH | `echo $PATH` | `$env:PATH -split ";"` |
| Ver si un programa está instalado y su versión | `python3 --version` | `python --version` |
| Ver la ayuda de un comando | `man ping` (sal con `q`) o `ping --help` | `Get-Help ping` o `ping /?` |

### Abrir programas y webs

| Quiero... | Mac | Linux | Windows |
|---|---|---|---|
| Abrir una web en el navegador | `open https://github.com` | `xdg-open https://github.com` | `start https://github.com` |
| Abrir una aplicación | `open -a "Calculator"` | `gnome-calculator &` | `calc` |
| Abrir un archivo con su programa | `open informe.pdf` | `xdg-open informe.pdf` | `start informe.pdf` |
| Abrir el explorador aquí | `open .` | `xdg-open .` | `explorer .` |

### Sistema, red y procesos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Espacio libre en disco | `df -h` | `Get-PSDrive C` |
| Comprobar si hay conexión con una web | `ping -c 4 github.com` | `ping github.com` |
| Ver mi IP local | Mac: `ipconfig getifaddr en0` · Linux: `hostname -I` | `ipconfig` |
| Descargar una página o un archivo | `curl -O https://...` | `curl.exe -O https://...` |
| Ver programas en ejecución | `top` (sal con `q`) | `Get-Process \| sort CPU -Desc \| select -First 10` |
| Buscar un proceso por nombre | `ps aux \| grep -i calc` | `Get-Process *calc*` |
| Cerrar un proceso | `kill 1234` (número de proceso) | `Stop-Process -Id 1234` |
| Cerrar un proceso por nombre | `pkill -i calculator` | `Stop-Process -Name CalculatorApp` |
| Fecha y hora | `date` | `Get-Date` |
| Parar un comando que no termina | **Ctrl + C** | **Ctrl + C** |

### Gestores de paquetes (instalar programas por terminal)

| Sistema | Gestor | Ejemplo |
|---|---|---|
| Windows | `winget` (viene instalado) | `winget search vlc` · `winget install VideoLAN.VLC` |
| macOS | `brew` (Homebrew, se instala aparte) | `brew install wget` |
| Ubuntu / Debian | `apt` | `sudo apt install tree` |

`sudo` (Linux y Mac) ejecuta un comando **como administrador**. Te pedirá tu contraseña. Mientras la escribes no aparece nada en pantalla: es normal.

---

## 🧪 Pruébalo

**1. Un comando es un programa.**

Mac / Linux: `which ls`
Windows: `Get-Command ls`

✅ Mac: `/bin/ls`. Linux: `/usr/bin/ls`. Es la ruta del programa. Windows: `ls` es un **alias** de `Get-ChildItem`. PowerShell usa nombres largos y ofrece abreviaturas parecidas a las de Linux para que sea más cómodo.

**2. ¿Qué tengo instalado?** Prueba estos comandos uno a uno:
```
git --version
python3 --version
node --version
```
En Windows, prueba `python --version` en lugar de `python3`.
✅ Unos mostrarán una versión. Otros, `command not found`: ese programa no está instalado o no está en el PATH.
- **Mac:** si `git` o `python3` abren una ventana para instalar las *herramientas de desarrollo*, pulsa **Instalar**. Es lo que instala Git para el módulo 6.
- **Windows:** si `python` abre la Microsoft Store o no muestra nada, es que no está instalado. Cierra la Store y sigue.

**3. Abre una web y una aplicación desde la terminal.**

| Mac | Linux | Windows |
|---|---|---|
| `open https://github.com` | `xdg-open https://github.com` | `start https://github.com` |
| `open -a "Calculator"` | `gnome-calculator &` | `calc` |

✅ Se abren el navegador y la calculadora. La CLI también controla la GUI.

**4. Encuentra la calculadora entre los procesos y ciérrala desde la terminal.**

Mac: `pkill -i calculator`
Linux: `pkill gnome-calculator`
Windows: `Get-Process *calc*` para ver el nombre, y después `Stop-Process -Name CalculatorApp`

✅ La calculadora se cierra. Así se cierra un programa colgado cuando la interfaz gráfica no responde.

**5. Comprueba la conexión a internet.**

Mac / Linux: `ping -c 4 github.com`
Windows: `ping github.com`

✅ Cuatro líneas con un tiempo en milisegundos (`time=25 ms`). Si sale `Unknown host` o `timeout`, no hay conexión con ese servidor.
Prueba también `ping github.com` en Mac o Linux **sin** `-c 4`: no para nunca. Detenlo con **Ctrl + C**.

**6. ¿Cuánto disco te queda?**

Mac / Linux: `df -h`
Windows: `Get-PSDrive C`

✅ Mac/Linux: busca la línea de `/` o `/System/Volumes/Data`, columna `Avail`. Windows: columna `Free`, en GB.

**7. Tu primer script.** Un script es un archivo con comandos que se ejecutan en orden.

Mac / Linux (en Linux en español, cambia `Downloads` por `Descargas`):
```
cd ~/taller
echo 'echo "Usuario: $USER"' > informe.sh
echo 'date' >> informe.sh
echo 'df -h ~' >> informe.sh
echo 'ls ~/Downloads | wc -l' >> informe.sh
cat informe.sh
bash informe.sh
```

Windows:
```
cd ~/taller
echo 'Write-Output "Usuario: $env:USERNAME"' > informe.ps1
echo 'Get-Date' >> informe.ps1
echo 'Get-PSDrive C' >> informe.ps1
echo '(ls ~/Downloads).Count' >> informe.ps1
cat informe.ps1
.\informe.ps1
```

✅ Con un solo comando se ejecutan los cuatro. Fíjate en las **comillas simples** al crear el script: evitan que `$USER` se sustituya al escribir el archivo, para que se sustituya al ejecutarlo.

> [!NOTE]
> **Windows:** si aparece *"la ejecución de scripts está deshabilitada en este sistema"*, es una medida de seguridad. Permite los scripts creados por ti con:
> ```
> Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
> ```
> Responde `S` (o `Y`) y vuelve a ejecutar `.\informe.ps1`.
>
> Si es un ordenador de empresa y no te deja cambiarlo, ejecútalo así: `powershell -ExecutionPolicy Bypass -File .\informe.ps1`

**8. Hazlo ejecutable (Mac / Linux).**
```
chmod +x informe.sh
./informe.sh
```
✅ Funciona sin escribir `bash` delante. `chmod +x` da permiso de ejecución. `./` significa "el programa que está en esta carpeta", porque `~/taller` no está en el PATH.

---

## ⚠️ Errores típicos

| Ves esto | Qué pasa | Qué hacer |
|---|---|---|
| `command not found` justo después de instalar algo | La terminal no ha recargado el PATH | Cierra la terminal y ábrela de nuevo |
| `Permission denied` al ejecutar `./informe.sh` | El archivo no tiene permiso de ejecución | `chmod +x informe.sh` |
| `informe.sh: command not found` | Falta `./` delante | `./informe.sh` |
| `curl` da un error raro en Windows | En PowerShell 5, `curl` es un alias de otro comando | Usa `curl.exe` |
| `sudo` pide contraseña y no se ve lo que escribes | Es normal, por seguridad | Escríbela y pulsa Enter |
| `ping` no termina (Linux / Mac) | Por defecto es infinito | **Ctrl + C**, o usa `-c 4` |

---

## 🎯 Reto: diagnóstico del equipo

⏱️ 8 min

Imagina que das soporte técnico por videollamada. Una persona comparte pantalla y la otra le **dicta** los comandos para averiguar:

1. El nombre de usuario.
2. El sistema operativo y su versión.
3. El espacio libre en disco.
4. Si hay conexión con `github.com` y cuántos milisegundos tarda.
5. Si tiene Git instalado y qué versión.
6. Los 3 programas que más CPU consumen ahora mismo.

Después, cambiad los papeles.

✅ **Comprueba:** quien dicta ha conseguido las 6 respuestas sin tocar el ordenador de la otra persona. Así funciona el soporte técnico remoto real.



---

[⬅️ Anterior](04-leer-y-buscar.md) · [Siguiente: Git, tu propia copia ➡️](06-git-clonar-y-fork.md)
