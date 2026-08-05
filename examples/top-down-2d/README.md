# Example: Top-Down 2D

Referencia de cómo aplicar la skill `unity-rapid-prototyping` a un juego top-down 2D.

## Core loop

Moverse por el mapa + interactuar con el entorno (recoger / atacar / hablar).

## Gate aplicado a las primeras features

| Feature | Veredicto | Por qué |
|---------|-----------|---------|
| Movimiento 8 direcciones | ✅ AHORA | Es el core loop |
| Cámara que sigue al jugador | ✅ AHORA | Sin cámara no se juega |
| Sistema de inventario | ⏸ NO AHORA | Sirve al loop pero no es <1h; placeholder: recoger = contador |
| Árbol de diálogos | ⏸ NO AHORA | Asset (Dialogue System) o placeholder: panel de texto |
| Mapa procedural | ❌ NUNCA (por ahora) | No sube chances de terminar; mapa a mano primero |

## Prototipo mínimo

- 1 escena, cámara ortográfica siguiendo al player
- Player: cubo/capsule con controller top-down (placeholders)
- 1 target interactivo (recoger/atacar)
- Lógica de reglas en pure C# (testeable en EditMode)

## Cómo iterar

1. Play mode con 1 objeto jugable y 1 target
2. Compile check en cada cambio de script
3. Cuando el loop divierte → recién ahí arte/juice
