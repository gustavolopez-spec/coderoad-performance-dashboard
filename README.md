# CodeRoad Internal — Performance Dashboard

Dashboard interno de tracking, performance, LOE y capacidad del equipo de
operaciones de CodeRoad Internal (WOMS, Salesforce, SFX, Smartsheet y otras
fuentes). Es un archivo unico (`index.html`) que corre entero en el
navegador — no hay servidor ni base de datos, todo se procesa localmente
al abrir la pagina.

## Como ver el dashboard

Entra directamente a la version publicada:

`https://gustavolopez-spec.github.io/coderoad-performance-dashboard/`

Al abrirla, el dashboard revisa automaticamente la carpeta `datos/` de
este repositorio y carga los archivos Excel que encuentre ahi. No hace
falta subir nada manualmente desde el navegador.

## Estructura de carpetas

Dentro de `datos/` hay una carpeta por periodo:

- `Historicos` — todo lo anterior a agosto 2026, ya cargado, no se toca.
- `Agosto 2026` — ya cargada.
- `Septiembre 2026`, `Octubre 2026`, `Noviembre 2026`, `Diciembre 2026`,
  `Enero 2027`, `Febrero 2027`, `Marzo 2027`, `Abril 2027`, `Mayo 2027`,
  `Junio 2027`, `Julio 2027`, `Agosto 2027` — creadas de antemano y vacias,
  esperando los archivos de cada mes.

Si en algun momento se necesita una carpeta de un mes mas adelante que no
este creada todavia, se crea igual que cualquier carpeta nueva en GitHub
("Add file" > "Create new file", escribiendo la ruta completa, por ejemplo
`Septiembre 2028/nombre-archivo.xlsx`).

## Como subir los datos del mes (equipo)

1. Entra a la carpeta `datos/` de este repositorio.
2. Entra a la carpeta del mes correspondiente (ejemplo: `Septiembre 2026`).
3. Subi ahi tu archivo Excel del mes, manteniendo el mismo patron de
   nombre que se usa siempre (cambiando solo el mes), por ejemplo
   `CR Internal - LP Sep 26.xlsx`.
4. Listo. El dashboard lo va a detectar solo la proxima vez que se abra
   (o se recargue), normalmente en cuestion de segundos a un par de
   minutos.

### Reglas importantes

- **No modifiques ni borres archivos de meses anteriores**, incluida la
  carpeta `Historicos`. Son historial — si encontras un error en un mes
  pasado, avisale a Gus en vez de reemplazar el archivo directamente.
- **Cada persona sube unicamente el archivo que le corresponde** (ver
  tabla abajo). No subas ni reemplaces el archivo de otra fuente.
- El nombre y la fecha de quien subio cada archivo queda registrado
  automaticamente en el historial de GitHub (pestana "Commits" del
  repositorio o del archivo puntual) — no hace falta anotarlo aparte.

### Quien sube que

| Archivo (fuente) | Sistema origen | Responsable |
|---|---|---|
| CR Internal - Site Services | SFX | Victor Mollinedo |
| CR Internal - Postings | SFX | Victor Mollinedo |
| 4 Other projects | Smartsheet | Victor Mollinedo |
| CR Internal - LP (Landing Pages) | WOMS | Gus |
| CR Int - Reworks | WOMS | Gus |
| CR Int - CW (Copywriters) | WOMS | Gus |
| CR Int Prem SEO (Premium SEO) | WOMS | Gus |

Nota: dos responsables en total para simplificar la coordinacion —
Victor cubre todo lo que sale de SFX y Smartsheet, y Gus cubre todo lo
que sale de WOMS. Si algun mes alguno de los dos no puede subir los
suyos, que se coordine puntualmente ese mes.

## Notas tecnicas (para quien mantenga el dashboard)

- El dashboard detecta el tipo de cada archivo por su contenido (headers
  de columnas), no por el nombre del archivo ni por el nombre de la
  carpeta — cualquier carpeta dentro de `datos/` es leida, sin importar
  como se llame.
- La carga automatica desde GitHub usa la API publica de GitHub (sin
  token, porque el repositorio es publico). Esta configurada en
  `index.html` bajo `GITHUB_AUTOLOAD` (owner, repo, branch, carpeta de
  datos).
- Cuando el dueno del dashboard (Gus) lo abre, ademas de cargar los
  datos nuevos automaticamente, se le muestra el mismo panel de vista
  previa que aparece al subir un archivo a mano (resumen de filas
  nuevas/duplicadas y alertas de calidad de datos), para poder
  confirmar antes de que se guarden. El resto del equipo no ve ese
  panel — para ellos, subir el archivo a la carpeta es el unico paso.
