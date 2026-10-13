# 3️⃣ Copiar, mover y borrar

⏱️ 25 min · [⬅️ Anterior](02-crear.md) · [Inicio](../README.md) · [Siguiente ➡️](04-leer-y-buscar.md)

## La idea

Crear es fácil. Lo que de verdad ahorra tiempo es **reorganizar**: mover 200 archivos con un solo comando, copiar una plantilla, renombrar, limpiar.

Los **comodines** son la clave. `*` significa "cualquier cosa". Con `*.pdf` seleccionas todos los PDF de una carpeta de una vez.

> [!WARNING]
> **`rm` no usa la papelera.** Lo que borras desde la terminal desaparece. Antes de borrar, comprueba con `pwd` dónde estás y con `ls` qué vas a borrar.

## Los comandos

| Quiero... | Mac / Linux | Windows (PowerShell) |
|---|---|---|
| Copiar un archivo | `cp origen.txt copia.txt` | `cp origen.txt copia.txt` |
| Copiar un archivo a otra carpeta | `cp informe.pdf archivo/` | `cp informe.pdf archivo/` |
| Copiar una carpeta entera | `cp -r plantilla nueva` | `cp -r plantilla nueva` |
| Mover un archivo a otra carpeta | `mv informe.pdf archivo/` | `mv informe.pdf archivo/` |
| **Renombrar** | `mv viejo.txt nuevo.txt` | `mv viejo.txt nuevo.txt` |
| Borrar un archivo | `rm borrador.txt` | `rm borrador.txt` |
| Borrar una carpeta vacía | `rmdir carpeta` | `rmdir carpeta` |
| Borrar una carpeta **con todo** | `rm -r carpeta` | `rm -r carpeta` |
| Borrar preguntando uno a uno | `rm -i *.txt` | `rm *.txt -Confirm` |
| Ver qué se borraría sin borrar | `ls *.tmp` | `rm *.tmp -WhatIf` |

**Comodines:**

| Patrón | Selecciona | Ejemplo |
|---|---|---|
| `*` | Cualquier cosa | `*` = todo lo que hay en la carpeta |
| `*.pdf` | Todo lo que acaba en `.pdf` | `mv *.pdf facturas/` |
| `factura-*` | Todo lo que empieza por `factura-` | `ls factura-*` |
| `*2026*` | Todo lo que contiene `2026` | `cp *2026* archivo-2026/` |
| `?` | Un solo carácter cualquiera | `ls informe-?.docx` → `informe-1`, `informe-2`... |

💡 **`mv` sirve para dos cosas.** Si el destino es una carpeta que existe, **mueve**. Si no, **renombra**.

💡 **Buena práctica:** antes de `mv *.pdf ...` o `rm *.tmp`, ejecuta `ls *.pdf` o `ls *.tmp`. Así ves exactamente qué archivos vas a tocar.

---

## 🧪 Pruébalo

Trabaja en el proyecto que creaste en el módulo 2.
```
cd ~/taller/mi-proyecto
```

**1. Haz una copia de seguridad de un archivo antes de tocarlo.** Es lo primero que hace cualquier persona técnica antes de editar algo importante.
```
cp README.md README.md.bak
ls
```
✅ Hay dos archivos con el mismo contenido. Compruébalo con `cat README.md.bak`.

**2. Renombra.**
```
mv README.md.bak README-backup.md
ls
```
✅ `README.md.bak` ya no existe. Ahora se llama `README-backup.md`.

**3. Mueve a otra carpeta.**
```
mkdir backups
mv README-backup.md backups/
ls
ls backups
```
✅ El archivo ya no está en la raíz del proyecto. Está en `backups`.

**4. Copia una carpeta entera.** Duplica el proyecto para tener una versión de pruebas.
```
cd ~/taller
cp -r mi-proyecto mi-proyecto-pruebas
ls
ls mi-proyecto-pruebas
```
✅ Dos proyectos idénticos. Puedes romper la copia sin tocar el original.

**5. Borra un archivo.**
```
rm mi-proyecto-pruebas/docs/notas.txt
ls mi-proyecto-pruebas/docs
```
✅ `notas.txt` ya no está. Y no está en la papelera.

**6. Borra una carpeta vacía y una con contenido.**
```
rmdir mi-proyecto-pruebas
```
✅ Mac y Linux: error, la carpeta **no está vacía**. `rmdir` te protege.
Windows: en vez de un error, PowerShell **pregunta** si quieres borrarla con todo su contenido. Responde `N` y Enter. Es su forma de protegerte.

Ahora sí, bórrala:
```
rm -r mi-proyecto-pruebas
ls
```
✅ La copia ha desaparecido con todo su contenido. Por eso `rm -r` es el comando más delicado del día.

---

## ⚠️ Errores típicos

| Ves esto | Qué pasa | Qué hacer |
|---|---|---|
| `cp: -r not specified; omitting directory` | Intentas copiar una carpeta sin `-r` | `cp -r carpeta destino` |
| `Directory not empty` · `El directorio no está vacío` | `rmdir` solo borra carpetas vacías | `rm -r carpeta`, tras comprobar con `ls` |
| Windows pide confirmación al borrar una carpeta | PowerShell avisa si tiene contenido | Escribe `S` (o `Y`) y Enter, o usa `rm -r` |
| `rm -rf` da error en Windows | PowerShell no admite `-rf` junto | Usa `rm -r -Force carpeta` |
| `mv` ha "desaparecido" un archivo | Lo has renombrado en lugar de moverlo, porque la carpeta destino no existía | `ls`: tendrás un archivo con el nombre de la carpeta. Crea la carpeta y muévelo |
| Mac: `zsh: sure you want to delete all the files?` | Has escrito `rm *` | Responde `n` salvo que estés totalmente segura/o |

---

## 🎯 Reto: ordenar una carpeta de Descargas

👥 Salas de Zoom de 2-3 personas · ⏱️ 12 min

La carpeta de Descargas de casi cualquier persona acaba así: facturas, nóminas, contratos, fotos, hojas de cálculo, instaladores viejos y archivos temporales mezclados. Vas a ordenar una copia de prueba **solo con la terminal**.

**1. Prepara el escenario.** Copia el bloque de tu sistema, pégalo en la terminal y pulsa Enter.

Windows: si aparece un aviso de que vas a pegar varias líneas, pulsa **Pegar de todos modos**.

Mac / Linux:
```
mkdir -p ~/taller/descargas-prueba
cd ~/taller/descargas-prueba
touch factura-2026-01-proveedor.pdf factura-2026-02-proveedor.pdf factura-2026-03-luz.pdf factura-2025-12-luz.pdf
touch nomina-2026-01.pdf nomina-2026-02.pdf nomina-2026-03.pdf
touch contrato-alquiler-local.pdf contrato-mantenimiento.docx contrato-laboral-borrador.docx
touch evento-presentacion-01.jpg evento-presentacion-02.jpg evento-presentacion-03.jpg logo-empresa.png
touch presupuesto-2026.xlsx gastos-t1-2026.xlsx clientes-activos.csv
touch acta-reunion-enero.docx acta-reunion-febrero.docx
touch borrador-acta.tmp informe-temporal.tmp cache-01.tmp cache-02.tmp instalador-antiguo.dmg
ls
```

Windows:
```
mkdir ~/taller/descargas-prueba
cd ~/taller/descargas-prueba
ni factura-2026-01-proveedor.pdf, factura-2026-02-proveedor.pdf, factura-2026-03-luz.pdf, factura-2025-12-luz.pdf
ni nomina-2026-01.pdf, nomina-2026-02.pdf, nomina-2026-03.pdf
ni contrato-alquiler-local.pdf, contrato-mantenimiento.docx, contrato-laboral-borrador.docx
ni evento-presentacion-01.jpg, evento-presentacion-02.jpg, evento-presentacion-03.jpg, logo-empresa.png
ni presupuesto-2026.xlsx, gastos-t1-2026.xlsx, clientes-activos.csv
ni acta-reunion-enero.docx, acta-reunion-febrero.docx
ni borrador-acta.tmp, informe-temporal.tmp, cache-01.tmp, cache-02.tmp, instalador-antiguo.exe
ls
```

**2. Organiza.** Al terminar, la carpeta debe quedar así:

```
descargas-prueba/
├── facturas/
│   ├── 2025/      → la factura de 2025
│   └── 2026/      → las facturas de 2026
├── nominas/
├── contratos/
├── actas/
├── imagenes/
└── hojas-calculo/ → .xlsx y .csv
```

Y además:
- Los archivos `.tmp` y el instalador antiguo, **borrados**.
- En la raíz de `descargas-prueba` **no queda ningún archivo suelto**, solo carpetas.


✅ **Comprueba:**
- `ls` en `descargas-prueba` muestra solo las 6 carpetas.
- `ls facturas/2026` muestra 3 archivos.
- Mac/Linux: `ls *.tmp` da error, porque ya no existen.

<details>
<summary>💡 Pista</summary>

Orden recomendado: primero crea todas las carpetas. Después mueve por patrón, de lo más concreto a lo más general. Por ejemplo, mueve `factura-2025-*` antes que `factura-*`. Antes de cada `mv` con comodín, haz `ls` con el mismo patrón para ver qué vas a mover.
</details>

<details>
<summary>💡 Solución (Mac / Linux)</summary>

```
mkdir -p facturas/2025 facturas/2026 nominas contratos actas imagenes hojas-calculo
mv factura-2025-* facturas/2025/
mv factura-2026-* facturas/2026/
mv nomina-* nominas/
mv contrato-* contratos/
mv acta-* actas/
mv *.jpg *.png imagenes/
mv *.xlsx *.csv hojas-calculo/
ls *.tmp *.dmg
rm *.tmp *.dmg
ls
```
</details>

<details>
<summary>💡 Solución (Windows)</summary>

```
mkdir facturas/2025, facturas/2026, nominas, contratos, actas, imagenes, hojas-calculo
mv factura-2025-* facturas/2025/
mv factura-2026-* facturas/2026/
mv nomina-* nominas/
mv contrato-* contratos/
mv acta-* actas/
mv *.jpg imagenes/
mv *.png imagenes/
mv *.xlsx hojas-calculo/
mv *.csv hojas-calculo/
rm *.tmp -WhatIf
rm *.tmp
rm *.exe
ls
```
</details>

---

[⬅️ Anterior](02-crear.md) · [Siguiente: Leer y buscar ➡️](04-leer-y-buscar.md)
