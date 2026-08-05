# Example: Survivors (horda)

Referencia de cómo aplicar la skill `unity-rapid-prototyping` a un survivor-like (horda infinita, auto-ataque, subir de nivel).

## Core loop

Sobrevivir oleadas de enemigos que te persiguen, mientras el auto-ataque hace daño; subir de nivel al acumular XP; cada nivel elige un upgrade.

## Gate aplicado a las primeras features

| Feature | Veredicto | Por qué |
|---------|-----------|---------|
| Movimiento del player | ✅ AHORA | Base de todo |
| Enemigos que te persiguen (seeking simple) | ✅ AHORA | El loop empieza cuando te persiguen |
| Auto-ataque (timer + daño en área) | ✅ AHORA | Tercer pilar del loop |
| Sistema de niveles + upgrades | ⏸ NO AHORA | El loop divierte sin él; placeholder: daño sube solo |
| XP / orbes | ⏸ NO AHORA | Contador simple primero |
| Oleadas con dificultad creciente | ⏸ NO AHORA | Spawner con timer — placeholder |
| Variedad de enemigos | ⏸ NO AHORA | 1 tipo primero, después variantes |
| "Juice" (partículas, shake) | ❌ NUNCA (por ahora) | Hasta que el loop base divierta |

## Prototipo mínimo

- 1 escena grande/abierta
- Player con movimiento (placeholder) + auto-ataque por timer
- Spawner de enemigos con seeking simple (rigidbody + look-at + move)
- Contador de kills como única "meta" inicial
- Reglas (daño, vida, spawn) en pure C# testeable en EditMode

## Detalle clave del género

El "se siente bien" acá es el **crescendo**: spawner que se acelera, kills que dan feedback inmediato. Se valida en play mode; los tests EditMode cubren el cálculo de spawn/dificultad en pure C#.
