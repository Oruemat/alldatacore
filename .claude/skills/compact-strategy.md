# Skill: Compact Strategy

## Propósito
Qué preservar y qué descartar al compactar, según el tipo de proyecto.

---

## Trigger de compactación
Compactar cuando:
- Claude Code sugiere compactación (70% contexto)
- El usuario dice `/compact`
- La conversación supera ~20 intercambios

---

## Siempre preservar (todos los proyectos)

### 1. Estado del proyecto
```
- Contenido del STATE.md activo
- Fase actual y qué se está haciendo
- Pendientes no completados
```

### 2. Decisiones tomadas en esta sesión
```
- "Decidimos usar X en vez de Y porque..."
- "El usuario confirmó que prefiere..."
- "Descartamos el approach de... porque..."
```

### 3. Archivos modificados
```
- Path de cada archivo tocado
- Qué se cambió (resumen, no diff completo)
- Si el build pasó o no
```

### 4. Errores y fixes
```
- Errores que aparecieron y cómo se resolvieron
- Workarounds aplicados
```

### 5. Contexto del usuario
```
- Lo que el usuario pidió originalmente
- Restricciones que mencionó
- Preferencias expresadas
```

---

## Siempre descartar

### 1. Contenido completo de archivos leídos
El contenido de archivos se puede re-leer. Preservar solo el path y un resumen de qué contiene si es relevante.

### 2. Output de builds exitosos
Si el build pasó, no preservar el output completo. Solo "build OK".

### 3. Intentos fallidos ya resueltos
Si probaste 3 approaches y el tercero funcionó, descartar los primeros dos. Solo preservar: "Intenté X e Y, fallaron por Z. Funciona con approach W."

### 4. Explicaciones largas ya procesadas
Si Claude explicó un concepto y el usuario respondió "ok", el concepto no necesita preservarse.

---

## Específico por proyecto

### Landing / Portfolio
- Preservar: rutas afectadas, componentes modificados, estado de deploy
- Descartar: contenido HTML/JSX completo, estilos CSS leídos

### POS (Sistema de Gestión)
- Preservar: migraciones SQL pendientes, cambios en tablas/RLS, estado de branch_stock
- Descartar: output de queries, contenido de componentes no modificados

### Studio
- Preservar: estado de los dos prompts (handlers.ts y design-prompt.ts), si están sincronizados
- Descartar: JSON de compositions generadas, output de Remotion

### Workspace
- Preservar: proyecto de cliente activo, requisitos, estado de skills ejecutadas
- Descartar: output de builds de clientes, contenido de templates

---

## Formato de compactación

Al compactar, el resumen debe seguir esta estructura:
```
## Sesión compactada — {proyecto}

### Objetivo: [qué se está haciendo]
### Estado: [dónde quedamos]
### Archivos modificados: [lista con resumen]
### Decisiones: [lista]
### Pendientes: [lista]
### Errores resueltos: [lista breve]
### Notas: [cualquier cosa que la próxima iteración necesita saber]
```
