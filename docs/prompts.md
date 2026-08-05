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

## Reglas de uso

- Pedí el veredicto del gate por escrito: fuerza al agente a decidir antes de codear
- Timeboxeá todo sprint: "2 horas", "1 hora enfocada"
- Si el agente propone código sin pasar por el gate → recordárselo explícitamente
