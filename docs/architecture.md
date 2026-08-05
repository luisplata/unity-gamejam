# Architecture — mínima, orientada a validar el core loop

## Regla de oro

La arquitectura existe para acelerar la iteración, no para la mantenibilidad a largo plazo. En un jam: **una escena, MonoBehaviours planos, referencias directas.**

## Qué evitar

- ❌ DI containers / IoC
- ❌ Event buses / message brokers
- ❌ "Sistemas extensibles" para features hipotéticas
- ❌ Capas de abstracción sin un segundo consumidor real

## Qué usar

- ✅ `MonoBehaviour` planos con referencias serializadas directas
- ✅ Una sola escena de juego (más una de menú si hace falta)
- ✅ `ScriptableObject` solo para tuning (stats, config) que quieras cambiar sin tocar código
- ✅ Lógica pura (reglas del juego) fuera de los MonoBehaviours, para poder testearla en EditMode

## Lógica pura vs. MonoBehaviour

```
Reglas del juego (pure C#)  ←→  testable en EditMode (rápido)
        ↑ usa
MonoBehaviours (capa Unity) ←→  input, transform, física, MCP
```

Ejemplo: `Health` es una clase plana; el `MonoBehaviour` solo la conecta con el mundo (colliders, UI).

## Placeholders son features

- Cubos/capsules/esferas en vez de arte
- Sprites blancos o de color plano en vez de texturas
- Sonidos/partículas SOLO cuando el loop ya divierte

## Cuándo se permite más arquitectura

Solo cuando hay dolor real: dos consumidores del mismo código, o un bug de estado que el código plano no puede contener. Se introduce incrementalmente, nunca preventivamente.
