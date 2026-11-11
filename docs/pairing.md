# El par: divergir antes de validar

> Este archivo es una **proyección, no una fuente**. Si algo no coincide con `skills/*/SKILL.md`, mandan los skills. Y nada de lo que hay acá se carga en tiempo de ejecución: es para leer en GitHub.

Una **decide**, la otra **abre opciones**. Ninguna hace el trabajo de la otra y ninguna necesita que la otra exista.

## La secuencia

UR es dueño de todos los estados; CF es una subrutina que se llama y vuelve. El reloj, el anuncio y el veredicto nunca cambian de manos.

```text
[IDLE] ──el usuario cuenta el tema──► [PREFS]  UR: 5 preguntas, una por vez
                                          │
                       ┌──────────────────┴──────────────────┐
                  CF no está                             CF está
                       ▼                                     ▼
              [INLINE]  UR genera 3–5            [DIVERGE]  dueño: CF
                       │                          anuncia modo + minutos + objetivo
                       │                          método → recomendar y esperar
                       │                          ≤2 preguntas (0 si knowns completo)
                       │                                     ▼
                       │                             [RETURN]  CF devuelve el envelope
                       │                                     │
                       └──────────────────┬──────────────────┘
                                          ▼
                                     [CONVERGE]  UR: 6 criterios + veredicto
                                          │
              ┌───────────────┬───────────┴────────────┐
              ▼               ▼                        ▼
          BUILD NOW      VALIDATE FIRST              CUT
                              │                 queda tiempo?
                              ▼                 sí ───► [RECOVER]  2–3 combinaciones
                         [INSPECT]  Six Hats ≤2 por sombrero        │
                              └──────► re-gate (UR) ◄───────────────┘
```

Tres reglas que el dibujo encierra: **se mira antes de abrir** (sin CF, la palabra `creative-facilitator` no aparece); **que se acabe el tiempo no es un fracaso** (un pool de una idea es un cierre válido); **CUT es terminal**, salvo que quede tiempo para un `recover` o aparezca evidencia nueva.

## Quién decide qué

En la tabla, `UR` es el evaluador que invoca y `CF` es el facilitador convocado. Si instalás un solo skill, ese skill es el usuario y la otra columna no aparece.

| Decision | Owner | Rule |
|---|---|---|
| The 5 fixed preference questions | **UR** | CF reads `knowns`, never re-asks |
| Elastic questions (≤2) | **CF** | UR never asks them |
| Clock / `max_minutes` | **UR** | CF respects it, never extends it |
| Method choice | **CF** | recommend + wait; UR changes state, not method |
| Evaluation criteria | **UR** | CF never applies them |
| Verdict | **UR** | CF never emits one |
| Provenance assignment | **CF** | label at creation |
| Provenance preservation | **UR** | neither side re-labels what it received |
| Plan / backlog / tasks | **UR**, only after a verdict | CF never produces one |
| State announcement | **UR** | CF never switches mode itself |

## Los dos envelopes

Circulan como un bloque cercado cuya primera línea declara el tipo. Es lo único legible por máquina que hay en el repo: `envelope: cf-to-ur v1`.

### UR → CF

| Campo | Contenido |
|---|---|
| `challenge` | el tema o problema en una oración, confirmado |
| `knowns` | `genre_strength`, `jam_hours`, `team_size`, `csharp_level`, `must_haves`, `must_avoids` |
| `prior_attempts[]` | direcciones ya descartadas, con su causa |
| `max_minutes` | entero entre 20 y 40 |
| `mode` | `diverge` / `inspect` / `recover` |

CF no puede pedir ningún campo fuera de esa lista. Cuando uno falta, degrada el dato y sigue; nunca te devuelve la pelota pidiéndote el campo.

### CF → UR

| Clave | Forma |
|---|---|
| `pool[]` | `id, idea, provenance, cluster, derived_from` |
| `clusters[]` | `id, members, relation` — tres a cinco |
| `connections[]` | `ideas, why` — `why` en una oración |
| `open_questions[]` | huecos y supuestos que CF no resolvió |
| `suggested_next` | exactamente una oración, sólo sugerencia |

**CF no emite veredicto.** Fijate que `verdict` no está en la tabla: ni como clave, ni como prosa, ni como orden por calidad. Esa ausencia es el contrato, no un olvido.

## Las tres costuras

| Costura | Cuándo | Manda UR | Devuelve CF | Decide |
|---|---|---|---|---|
| i · después de las preferencias | siempre que CF esté instalado | `mode: diverge`, 25 min, los 5 campos | el envelope completo | UR: 6 criterios y veredicto |
| ii · `inspect` | una candidata en VALIDATE FIRST con riesgo conceptual | `mode: inspect` y la candidata | Six Hats ≤2 líneas por sombrero, con el tipo de evidencia si propone mover | UR vuelve a correr el gate |
| iii · `recover` | después de un CUT, con ≥20 min y primer CUT de esa dirección | `mode: recover` + el mecanismo muerto y su causa | 2–3 combinaciones, con fuente de restricción y mecanismo cambiado | UR re-evalúa; si ninguna pasa, sigue muerta |

Dos cosas que no se negocian: un `recover` por dirección, y una combinación sólo cuenta si **cambia el mecanismo** — arte nuevo o el mismo chiste con otro tema no cuentan.

## Cuando CF no está

UR se comporta **exactamente como antes**: sin envelope, sin error, sin warning, sin loop de reintento, sin nag para instalar nada. El camino inline es el flujo entero, no un fallback. El costo aceptado es uno: sin CF no tenés el pase de Forced Combination cuando todas las direcciones fallan Standout.

## Apéndice — chequeo de consistencia

Corré esto parado en la raíz del repo. Es el único CI que tenemos:

```bash
# A. el trigger de CF no compite con el de UR — esperá 0
awk 'NR>1 && /^---$/{exit} NR>1' skills/creative-facilitator/SKILL.md \
  | grep -inE 'game jam|core loop|prototype|prototipado|unity'

# B. UR conserva el trigger de jam — esperá game jam, core loop, prototipado
grep -nE 'game jam|core loop|prototipado' skills/unity-rapid-prototyping/SKILL.md

# C. vocabulario compartido, 5/5 en los dos archivos
for t in challenge divergence convergence provenance verdict; do
  printf '%s UR=%s CF=%s\n' "$t" \
    "$(grep -ci "$t" skills/unity-rapid-prototyping/SKILL.md)" \
    "$(grep -ci "$t" skills/creative-facilitator/SKILL.md)"
done

# D. la tabla de propiedad es la misma copia en los tres lugares — esperá 12
for f in skills/creative-facilitator/SKILL.md skills/unity-rapid-prototyping/SKILL.md docs/pairing.md; do sed -n '/^| Decision | Owner | Rule |/,/^| State announcement/p' "$f"; done | sort -u | wc -l
```
