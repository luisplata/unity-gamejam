# unity-rapid-prototyping

Skill de prototipado rápido para desarrollo de juegos en Unity a través del Unity MCP.

## De qué va

La mayoría de las skills enseñan **cómo programar**. Esta enseña **cómo decidir**: el agente actúa como un mentor de prototipado rápido que protege el core loop, el tiempo y las chances de terminar el juego.

Flujo completo de una game jam:

```
Tema + preferencias del usuario
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

## Instalación

### Opción 1 — Global (todos tus proyectos)

```bash
# Copiá la skill a la carpeta de skills de OpenCode (usuario)
mkdir -p ~/.config/opencode/skills/unity-rapid-prototyping
cp -r skills/unity-rapid-prototyping/* ~/.config/opencode/skills/unity-rapid-prototyping/
```

Queda disponible automáticamente en todos tus proyectos Unity.

### Opción 2 — Por proyecto (solo un juego)

```bash
# Copiá la skill al proyecto donde la vayas a usar
mkdir -p <tu-juego>/.opencode/skills/unity-rapid-prototyping
cp -r skills/unity-rapid-prototyping/* <tu-juego>/.opencode/skills/unity-rapid-prototyping/
```

Queda versionada junto al juego y solo se carga cuando trabajás en ese proyecto.

### Requisitos del proyecto Unity

La skill valida el entorno antes de proponer nada. El proyecto Unity necesita:

| Paquete | Cómo instalarlo |
|---------|-----------------|
| `com.coplaydev.unity-mcp` | Package Manager → Add from git URL → `https://github.com/CoplayDev/unity-mcp.git?path=/MCPForUnity#main` |
| `com.unity.ai.assistant` (Agentes.IA) | Package Manager → buscar "Assistant" (requiere Unity 6.0+ y proyecto vinculado a Unity Cloud) |
| `com.unity.test-framework` | Package Manager → instalar (para EditMode/PlayMode tests) |

Si falta alguno, la skill frena y te da el comando de instalación.

## Estructura

```
├── skills/
│   └── unity-rapid-prototyping/   # La skill (SKILL.md)
├── examples/                       # Referencias por género: gate aplicado
│   ├── top-down-2d/
│   ├── platformer/
│   └── survivors/
└── docs/
    ├── philosophy.md               # Por qué decidir > programar
    ├── architecture.md             # Arquitectura mínima para jam games
    ├── workflow.md                 # Flujo Unity MCP de iteración
    └── prompts.md                  # Templates de prompts para el agente
```

## License

Apache-2.0 — ver [LICENSE](LICENSE)
