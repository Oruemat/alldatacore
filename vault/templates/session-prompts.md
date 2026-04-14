# Prompts de Sesión — Uso Diario

## 1. Al iniciar sesión

### Prompt de arranque (copiar y pegar)
```
Lee vault/proyectos/{proyecto}/STATE.md y el último entry en vault/diario/. 
Resumí en 3 líneas: dónde quedamos, qué hay pendiente, y qué no tocar. 
No improvises — si no hay STATE, decime.
```

### Variante: retomar trabajo interrumpido
```
La sesión anterior se cortó por tokens. Lee vault/proyectos/{proyecto}/STATE.md 
y continuá con el primer pendiente. No repitas lo que ya está hecho.
```

### Variante: inicio de día con múltiples proyectos
```
Lee los STATE.md de vault/proyectos/. Listá el estado de cada proyecto 
en 1 línea y decime cuál tiene pendientes más urgentes.
```

---

## 2. Al cambiar de proyecto en la misma sesión

### Prompt de cambio
```
Cambiamos a {proyecto}. Lee vault/proyectos/{proyecto}/STATE.md. 
Contexto del proyecto anterior: [1 línea de lo que se hizo].
```

---

## 3. Al referenciar otro proyecto

### Prompt de cruce
```
Para este cambio necesito contexto del proyecto {otro_proyecto}. 
Lee vault/proyectos/{otro_proyecto}/STATE.md y decime cómo se 
relaciona con lo que estamos haciendo.
```

---

## 4. Al terminar una tarea

### Prompt de cierre de tarea
```
Tarea completada. Actualizá vault/proyectos/{proyecto}/STATE.md con: 
lo que se hizo, archivos modificados, pendientes actualizados, y notas 
para la próxima sesión.
```

---

## 5. Al terminar la sesión (antes del reset de tokens)

### Prompt de cierre de sesión
```
Sesión terminando. Ejecutá el flujo completo del memory-keeper:
1. Actualizar STATE.md del proyecto
2. Crear entry en vault/diario/ con fecha de hoy
3. Si hubo decisiones arquitecturales, crear en vault/decisiones/
4. Listar qué queda pendiente para la próxima sesión
```

---

## 6. Compactación

### Prompt de compactación manual
```
/compact — preservá: STATE.md activo, archivos modificados en esta sesión, 
decisiones tomadas, errores y fixes. Descartá: contenido de archivos leídos, 
output de builds exitosos, explicaciones ya procesadas.
```

---

## 7. Clasificación de cambios

### Prompt para activar el orquestador
```
Necesito: {descripción del cambio}. Clasificá complejidad y decime 
el flujo de agentes que vas a seguir.
```

### Variante: cambio mínimo directo
```
Cambio mínimo: {descripción}. Hacelo directo sin análisis.
```

---

## 8. Emergencias

### Prompt de rollback
```
El último cambio rompió {qué se rompió}. Revisá vault/proyectos/{proyecto}/STATE.md 
para ver qué archivos se tocaron y revertí solo lo necesario.
```

### Prompt de debug
```
Bug: {descripción}. Antes de tocar código, identificá la causa raíz 
leyendo los archivos relevantes. No hagas cambios hasta que entiendas qué pasa.
```
