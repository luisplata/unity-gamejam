# Workflow — iteración rápida con Unity MCP

## El bucle

```
cambio → compile check → play → confirmar diversión → commit
```

## Pasos

### 1. Estado del editor antes de tocar nada

Nunca construir sobre un compile roto:

```bash
read_console(types=["error"])        # errores de compilación/ejecución
# + revisar estado del editor (mcpforunity://editor/state)
```

### 2. Crear/modificar scripts

```bash
# Crear script vía MCP
create_script(path="Assets/Scripts/Player.cs", contents="...")

# COMPILE CHECK INMEDIATO — siempre
read_console(types=["error"])
```

Si hay errores: corregir antes de seguir. Los tipos/componentes nuevos no existen hasta que compila.

### 3. Validar

| Qué | Cómo |
|-----|------|
| Lógica (reglas del juego) | `run_tests(mode="EditMode")` + `get_test_job` |
| Feel (cómo se siente) | `manage_editor(action="play")` + screenshots |
| Escena | mínima: cámara, luz, objeto jugable, un target interactivo |

### 4. Confirmar contra el gate

¿La mecánica divierte? Si no: **kill or simplify**. Nunca pulir una mala idea.

### 5. Commit

Commits por unidad de trabajo entregable, con tests y docs junto al código que verifican. No commits por tipo de archivo.

## Reglas de oro

- Compile check después de CADA cambio de script
- Play mode para "se siente bien", EditMode tests para "funciona"
- Si una feature no entra en 1h enfocada → partirla o cortarla
- Placeholder > esperar arte
