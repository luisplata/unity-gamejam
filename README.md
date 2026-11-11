# Skills para game jams de Unity

Dos skills que se complementan: una **decide**, la otra **abre opciones**. Un mentor de prototipado rápido que protege el core loop, el tiempo y las chances de terminar el juego — y un facilitador de ideación que genera material crudo sin juzgarlo.

## De qué va

La mayoría de las skills enseñan **cómo programar**. Estas enseñan **cómo decidir**: el agente actúa como un mentor estricto que dice que NO a ~90% de las ideas, y como un facilitador que se encarga de que las ideas existan antes de matarlas.

Flujo completo de una game jam:

```
Tema + preferencias del usuario
        ↓
[DIVERGE]           → bloque con tiempo, sin juzgar (solo si instalás CF)
        ↓              método, ≤2 preguntas, pool con procedencia
   clusters[]       ── vuelven como 3-5 direcciones candidatas
        ↓
[Idea Validator]    → 3-5 direcciones, validadas contra 6 criterios
        ↓              (core loop, <1h, fun-risk, terminable, destacable, tema)
1 idea con core loop en una oración
        ↓
[Decision Gate]     → 5 preguntas antes de CADA feature
        ↓              (¿core loop? ¿<1h? ¿10x más simple? ¿asset? ¿termina?)
construcción + validación
        ↓
Gameplay-first      → grey-box > sistema limpio; placeholders son features;
arquitectura mínima → sin DI ni event buses; kill-or-simplify timebox
```

La división de trabajo: **la IA propone direcciones y pone disciplina; el humano decide con su gusto**. La IA es el mentor estricto, no el cerebro creativo.

## Las dos skills

| Skill | Qué hace | Se instala sola |
|---|---|---|
| `unity-rapid-prototyping` | Corre el reloj, hace las 5 preguntas fijas, aplica los 6 criterios y emite el veredicto (BUILD NOW / VALIDATE FIRST / CUT) | Sí — funciona completa por su cuenta |
| `creative-facilitator` | Corre un bloque de divergencia con tiempo, sin ranking ni veredicto, y devuelve un envelope con pool, clusters y conexiones | Sí — también sola, para cualquier problema |

**Las dos juntas son el flujo completo; cada una sirve sola.** Si instalás solo `unity-rapid-prototyping`, el flujo es exactamente el de siempre: no hay error, no hay warning, no hay nag para instalar nada.

**El costo aceptado de instalar una sola:** sin `creative-facilitator` no tenés el pase de Forced Combination cuando las 3-5 direcciones fallan el criterio Standout. Ese pase es lo único que agrega el par. Nada más cambia.

## Instalación

Una skill por comando. Todavía no hay un comando que instale las dos: son dos skills y dos instalaciones.

### Opción 1 — skills.sh CLI (recomendada)

Las skills están publicadas en este repo y se instalan con [skills.sh](https://skills.sh) (no requiere instalación previa, corre con npx):

```bash
npx skills add https://github.com/luisplata/unity-gamejam --skill unity-rapid-prototyping
npx skills add https://github.com/luisplata/unity-gamejam --skill creative-facilitator
```

El CLI detecta el `SKILL.md` en `skills/<nombre>/` y lo configura para tu agente. Para desactivar telemetría: `DISABLE_TELEMETRY=1`.

### Opción 2 — Global (todos tus proyectos)

```bash
# Copiá la skill de prototipado a la carpeta de skills de OpenCode (usuario)
mkdir -p ~/.config/opencode/skills/unity-rapid-prototyping
cp -r skills/unity-rapid-prototyping/* ~/.config/opencode/skills/unity-rapid-prototyping/

# Copiá la skill de ideación al mismo lugar
mkdir -p ~/.config/opencode/skills/creative-facilitator
cp -r skills/creative-facilitator/* ~/.config/opencode/skills/creative-facilitator/
```

Quedan disponibles automáticamente en todos tus proyectos Unity.

### Opción 3 — Por proyecto (solo un juego)

```bash
# Copiá la skill de prototipado al proyecto donde la vayas a usar
mkdir -p <tu-juego>/.opencode/skills/unity-rapid-prototyping
cp -r skills/unity-rapid-prototyping/* <tu-juego>/.opencode/skills/unity-rapid-prototyping/

# Copiá la skill de ideación al mismo proyecto
mkdir -p <tu-juego>/.opencode/skills/creative-facilitator
cp -r skills/creative-facilitator/* <tu-juego>/.opencode/skills/creative-facilitator/
```

Quedan versionadas junto al juego y solo se cargan cuando trabajás en ese proyecto.

### Requisitos del proyecto Unity

La skill de prototipado valida el entorno antes de proponer nada. El proyecto Unity necesita:

| Paquete | Cómo instalarlo |
|---------|-----------------|
| `com.coplaydev.unity-mcp` | Package Manager → Add from git URL → `https://github.com/CoplayDev/unity-mcp.git?path=/MCPForUnity#main` |
| `com.unity.ai.assistant` (Agentes.IA) | Package Manager → buscar "Assistant" (requiere Unity 6.0+ y proyecto vinculado a Unity Cloud) |
| `com.unity.test-framework` | Package Manager → instalar (para EditMode/PlayMode tests) |

Si falta alguno, la skill frena y te da el comando de instalación. `creative-facilitator` no necesita nada de esto: no toca Unity.

## Estructura

```
├── skills/
│   ├── unity-rapid-prototyping/    # Decide: core loop, gate, veredicto
│   │   └── SKILL.md
│   └── creative-facilitator/       # Diverge: bloque con tiempo, sin juzgar
│       ├── SKILL.md
│       └── templates/
│           └── session-record.md   # El record completo del modo workshop
├── examples/                       # Referencias por género: gate aplicado
│   ├── top-down-2d/
│   ├── platformer/
│   └── survivors/
└── docs/
    ├── philosophy.md               # Por qué decidir > programar
    ├── architecture.md             # Arquitectura mínima para jam games
    ├── workflow.md                 # Flujo Unity MCP de iteración
    ├── pairing.md                  # Cómo se hablan las dos skills
    └── prompts.md                  # Templates de prompts para el agente
```

## License

Apache-2.0 — ver [LICENSE](LICENSE)
