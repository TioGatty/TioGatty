# Runner iA 🏃

Entrenador de running con inteligencia artificial, construido sobre
[Claude Code](https://code.claude.com/) y su sistema de **skills**.

Arma planes de entrenamiento personalizados, registra lo que corriste, analiza cada semana
y te da recomendaciones para llegar a tu objetivo.

> Basado en [claude-running-coach](https://github.com/ColinEberhardt/claude-running-coach)
> de Colin Eberhardt (licencia MIT). Esta es la base sobre la que vamos a construir Runner iA.

## Qué hace

| Skill | Para qué sirve | Cómo pedírselo |
|---|---|---|
| `training-plan` | Plan de 5K, 10K, media maratón o maratón, semana por semana, con ritmos calculados | "Armame un plan de 10K para el 15 de diciembre, quiero bajar de 50 minutos" |
| `running-coach` | Compara lo planeado con lo que corriste y te da feedback | "Revisá mi semana 3" / "¿Cómo me fue esta semana?" |
| `strava-sync` | Importa tus actividades de Strava (necesita un conector MCP de Strava) | "Sincronizá la semana 2 desde Strava" |
| `training-dashboard` | Genera `dashboard.html` con tu progreso | "Mostrame el dashboard" |

Si no usás Strava, podés contarle tus entrenamientos a Claude, pegar un export de Garmin
u otra app, o escribir el archivo de la semana a mano en `training-log/`.

## Cómo usarlo

1. Abrí esta carpeta con Claude Code (en la terminal, el escritorio, la web o la app).
2. Las skills de `.claude/skills/` se cargan solas.
3. Pedí un plan en lenguaje natural. Claude te va a preguntar lo que le falte:
   distancia, fecha de la carrera, tiempo objetivo, km semanales actuales y días disponibles.

Todo se responde en español y en kilómetros (ver `CLAUDE.md`).

## Estructura

```
runner-ia/
├── CLAUDE.md                  # Instrucciones para Claude: idioma, unidades, archivos
├── .claude/skills/
│   ├── training-plan/
│   │   ├── SKILL.md
│   │   ├── references/coaches-guide.md   # Principios de entrenamiento
│   │   └── scripts/
│   │       ├── calculate_paces.py        # Zonas de ritmo a partir del tiempo objetivo
│   │       └── interval_calculator.py    # Distancia y tiempo total de una sesión de series
│   ├── running-coach/SKILL.md
│   ├── strava-sync/SKILL.md
│   └── training-dashboard/SKILL.md
├── training-log/              # week-N.md: lo que corriste cada semana
├── coaching-log/              # week-N-coaching-notes.md: análisis de cada semana
└── training-plan.md           # Se crea al pedir un plan
```

## Scripts

Requieren Python 3.8 o superior, sin dependencias externas.

```bash
# Ritmos para un 10K en 50:00
python3 .claude/skills/training-plan/scripts/calculate_paces.py -d 10 -t 50:00 --per-km

# Sesión: 2 km suaves + 5 x 1 km a 4:40 con 400 m de trote + 2 km suaves
python3 .claude/skills/training-plan/scripts/interval_calculator.py --unit km \
  --warmup 2km --intervals 5 --interval-dist 1km --interval-pace 4:40 \
  --recovery 400m --cooldown 2km --easy-pace 6:15
```

## Aviso

Runner iA no reemplaza a un entrenador ni a un médico. Escuchá a tu cuerpo y consultá a un
profesional antes de empezar un plan nuevo, sobre todo si tenés lesiones o problemas de salud.

## Licencia

MIT. Ver [LICENSE](LICENSE).
