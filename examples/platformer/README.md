# Example: Platformer

Referencia de cómo aplicar la skill `unity-rapid-prototyping` a un platformer.

## Core loop

Saltar + moverse horizontalmente por niveles con obstáculos.

## Gate aplicado a las primeras features

| Feature | Veredicto | Por qué |
|---------|-----------|---------|
| Salto (coyote time + jump buffer) | ✅ AHORA | Es el core loop, y se siente de inmediato |
| Movimiento horizontal | ✅ AHORA | Mitad del core loop |
| Gravedad / físicas | ✅ AHORA | Viene con el Rigidbody2D — no lo re-escribas |
| Enemigos con IA de patrulla | ⏸ NO AHORA | Placeholder: enemigo estático con collider |
| Checkpoints / respawn | ⏸ NO AHORA | Después del primer nivel jugable |
| Sistema de power-ups | ⏸ NO AHORA | Solo si el loop base ya divierte |
| Tilemap art | ❌ NUNCA (por ahora) | Placeholders: cubos/capsules |

## Prototipo mínimo

- 1 escena con suelo, un hueco, una plataforma
- Player: capsule con Rigidbody2D + salto (placeholder)
- 1 enemigo estático o patrulla simple
- Reglas (vidas, muerte, respawn) en pure C# testeable

## Detalle clave del género

El **feel del salto** (gravedad, coyote time, jump buffer) ES el juego. Se valida en play mode, no con tests. Tests EditMode: para reglas (vidas, condiciones de victoria), no para el feel.
