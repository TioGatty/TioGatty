# Runner iA

Entrenador de running con IA. Las skills viven en `.claude/skills/` y están basadas en
[claude-running-coach](https://github.com/ColinEberhardt/claude-running-coach) (MIT).

## Cómo trabajar en este proyecto

- **Idioma**: respondé siempre en español (Argentina). Los planes, los logs y las notas de
  coaching también se escriben en español, aunque las skills estén redactadas en inglés.
- **Unidades**: usá kilómetros y ritmos en min/km por defecto, salvo que el corredor pida millas.
  - `calculate_paces.py`: pasá siempre `--per-km`.
  - `interval_calculator.py`: pasá siempre `--unit km` y ritmos en min/km.
- **Scripts**: se ejecutan desde el directorio de la skill, por ejemplo
  `python3 .claude/skills/training-plan/scripts/calculate_paces.py -d 10 -t 50:00 --per-km`.
  Solo usan la librería estándar de Python 3.8+.

## Archivos que generan las skills

| Archivo | Skill que lo crea | Contenido |
|---|---|---|
| `training-plan.md` | `training-plan` | Plan completo, semana por semana |
| `training-log/week-N.md` | `strava-sync` o carga manual | Entrenamientos realizados en la semana N |
| `coaching-log/week-N-coaching-notes.md` | `running-coach` | Análisis y recomendaciones de la semana N |
| `dashboard.html` | `training-dashboard` | Panel de progreso |

Mantené estos nombres de archivo (en inglés) aunque el contenido esté en español: las skills
los buscan por nombre.

## Strava

La skill `strava-sync` necesita un servidor MCP de Strava conectado (herramientas
`mcp__strava__*`). Si no está disponible, pedile al corredor los datos de otra forma: que los
cuente, que pegue un export de Garmin/Strava, o que cargue el archivo en `training-log/` a mano.
