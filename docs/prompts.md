# Prompts — cómo pedirle al agente

Templates para sacarle el máximo al agente con la skill `unity-rapid-prototyping` cargada.

## 1. Pedir una feature (default)

> Quiero agregar [mecánica/feature] a [juego].
> Antes de proponer código, corré el Decision Gate y mostrame el veredicto por pregunta (core loop, <1h, 10x simpler, asset, odds de terminar).
> Si algo falla el gate, decímelo ANTES de escribir código.

## 2. Sprint de core loop

> Tenemos [tiempo, ej. 2 horas] para validar el core loop de [idea].
> Proponé el prototipo más chico posible (una escena, placeholders, un objeto jugable, un target) y construilo vía Unity MCP.
> Compile check en cada paso, play mode para confirmar.

## 3. Kill-or-simplify review

> Esta mecánica es [descripción]. Lleva [tiempo] y no me convence.
> Aplicá el gate: ¿la matamos, la simplificamos, o la dejamos? Justificá con las 5 preguntas.

## 4. Asset vs. custom

> Necesito [funcionalidad, ej. pathfinding, diálogos, inventario].
> ¿Existe un asset/paquete estándar que lo resuelva? Si sí, decime cuál y el costo aproximado de integrarlo vs. construirlo. Aplicá la pregunta 4 del gate.

## 5. Revisión de scope (anti-scope-creep)

> Lista de features candidatas: [lista].
> Clasificalas por prioridad contra el core loop y marcalas como AHORA / NO AHORA / NUNCA. Justificá con el gate.

## 6. Abrir el bloque de divergencia (UR → CF)

> Vamos a divergir antes de validar. Usá creative-facilitator en modo `diverge`, 25 minutos.
> challenge: [tema en una oración]
> knowns: genre_strength [género], jam_hours [horas], team_size [cuántos], csharp_level [beginner/comfortable/strong], must_haves [lista], must_avoids [lista]
> prior_attempts: [direcciones ya descartadas y por qué, o vacío]
> max_minutes: 25
> mode: diverge
> Devolveme el envelope con pool, clusters, connections, open_questions y suggested_next. No me digas cuál elegir.

## 7. Devolver el pool al Validator (CF → UR)

> Acá está el envelope que volvió del bloque: [pegá el bloque entero, desde `envelope: cf-to-ur v1`].
> Tratá cada cluster como una dirección candidata: pitch de una oración, acción de 10 segundos y lectura del tema.
> Corré los 6 criterios sobre cada una y emití BUILD NOW / VALIDATE FIRST / CUT por dirección. El veredicto es tuyo, no del pool.

## Reglas de uso

- Pedí el veredicto del gate por escrito: fuerza al agente a decidir antes de codear
- Timeboxeá todo sprint: "2 horas", "1 hora enfocada"
- Si el agente propone código sin pasar por el gate → recordárselo explícitamente
