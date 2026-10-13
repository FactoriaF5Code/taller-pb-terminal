# 0️⃣ Antes de empezar

⏱️ 15 min · [⬅️ Inicio](../README.md) · [Siguiente ➡️](01-orientarse.md)



## 1. Crear la cuenta de GitHub

**GitHub** es una web donde se guardan y comparten proyectos. Hoy la usamos para leer esta guía. Al final de la clase, para descargar el repositorio con Git.

1. Entra en **github.com** → botón **Sign up**.
2. **Email**: uno al que puedas entrar ahora. Te llegará un código.
3. **Password**: al menos 15 caracteres, o 8 con un número y una minúscula. 
4. **Username**: tu nombre público. Ejemplo: `pepa-lopez-dev`.
5. Resuelve el puzle de verificación y escribe el código que te llega al correo. Si no aparece, mira en **Spam**.
6. Si te hace preguntas sobre ti o te ofrece planes de pago, pulsa **Skip** o elige **Free**.



## 2. Abrir la terminal

| Mac | Linux (Ubuntu) | Windows |
|---|---|---|
| **Cmd + Espacio** → escribe `Terminal` → Enter | **Ctrl + Alt + T** | Tecla **⊞** → escribe `PowerShell` → Enter |

> [!IMPORTANT]
> **En Windows usa PowerShell**, no "Símbolo del sistema" (cmd). Si tienes **Terminal de Windows**, también vale: abre PowerShell por defecto.

✅ Cuando veamos `$`, `%` o `>`, y un cursor parpadeando. Esa línea se llama **prompt**. Significa: *"te escucho"*.

```
orwell@portatil ~ %                       ← Mac
orwell@portatil:~$                       ← Linux
PS C:\Users\orwell>                      ← Windows
```




## 3. Tu primer comando

Escribe esto en la terminal y pulsa **Enter**:

```
whoami
```

✅ Aparece tu **nombre de usuario** del ordenador. Acabas de hablar con tu ordenador escribiendo. 🎉

## 4. Comprueba que tu terminal está lista

Antes de seguir, confirma que todo funciona en **tu** sistema. Escribe los comandos de tu columna, uno a uno.

| Paso | Mac | Linux | Windows (PowerShell) |
|---|---|---|---|
| 1. ¿Dónde estoy? | `pwd` | `pwd` | `pwd` |
| 2. ¿Qué hay aquí? | `ls` | `ls` | `ls` |
| 3. ¿Puedo ver mis descargas? | `ls ~/Downloads` | `ls ~/Downloads` o `ls ~/Descargas` | `ls ~/Downloads` |
| 4. ¿Qué versión tengo? | `echo $SHELL` | `echo $SHELL` | `$PSVersionTable.PSVersion` |

✅ **Todo bien si:**
- `pwd` muestra tu carpeta personal y `ls` lista carpetas como `Desktop`, `Documents` o `Downloads`.
- El paso 3 muestra tus descargas, o nada si la carpeta está vacía. Ningún error.
- Mac: `/bin/zsh`. Linux: `/bin/bash`. Windows: un número que empieza por `5` o por `7`. Apúntalo: hay un par de comandos que cambian entre esas dos versiones.

⚠️ **Si algo falla:**

| Sistema | Ves esto | Qué hacer |
|---|---|---|
| Mac | Una ventana: *"Terminal quiere acceder a archivos de tu carpeta Descargas"* | Pulsa **Permitir**. Te lo preguntará también para Documentos y Escritorio |
| Mac | `Operation not permitted` | Pulsaste "No permitir". Ve a **Ajustes del Sistema → Privacidad y seguridad → Archivos y carpetas → Terminal** y activa las carpetas |
| Linux | `No such file or directory` con `~/Downloads` | Tu sistema está en español y la carpeta se llama de verdad `Descargas`. **Durante todo el taller, donde ponga `Downloads` escribe `Descargas`, y donde ponga `Documents`, `Documentos`** |
| Windows | El prompt no empieza por `PS` | Has abierto *Símbolo del sistema* (cmd). Escribe `powershell` y pulsa Enter |

> [!NOTE]
> En **Mac y Windows**, las carpetas se llaman `Desktop`, `Documents` y `Downloads` en la terminal, aunque el explorador las muestre en español. En **Linux** en español se llaman de verdad `Escritorio`, `Documentos` y `Descargas`.

Cuando los 4 pasos funcionen, reacciona con ✅ en Zoom.

Siguiente [módulo 1 ➡️](01-orientarse.md).
