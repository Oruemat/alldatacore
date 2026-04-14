# Skill: Token Efficiency

## Propósito
Las 8 reglas aplicadas como comportamiento por defecto. Cada regla incluye el anti-patrón que evita.

---

## Regla 1: Think before acting
**Hacer**: Usar `Think` para planificar qué archivos tocar antes de leer/editar cualquier cosa.
**Anti-patrón**: Leer 10 archivos "por las dudas" antes de entender qué se necesita.

## Regla 2: Be concise but thorough
**Hacer**: Responder con lo mínimo necesario. Si la respuesta es "listo, build OK", decir eso.
**Anti-patrón**: "He realizado los cambios solicitados. A continuación te explico detalladamente cada modificación que hice y por qué..."

## Regla 3: Prefer editing over rewriting
**Hacer**: `Edit` (str_replace) para cambiar las líneas específicas.
**Anti-patrón**: `Write` un archivo de 200 líneas porque cambiaron 5. Esto gasta tokens en output Y hace más difícil ver qué cambió.

### Cuándo SÍ reescribir
- Archivo nuevo
- Más del 70% del archivo cambia
- El archivo tiene <20 líneas

## Regla 4: No re-read unless changed
**Hacer**: Si leíste `store.ts` hace 3 turnos y nadie lo editó, usá tu memoria de contexto.
**Anti-patrón**: `Read store.ts` cada vez que se menciona Zustand.

### Excepción
Si el contexto se compactó y perdiste el contenido del archivo, re-leer es válido.

## Regla 5: Test before done
**Hacer**: Ejecutar `npm run build` o `npx tsc --noEmit` antes de reportar que terminaste.
**Anti-patrón**: "Los cambios deberían funcionar correctamente" sin verificar.

## Regla 6: No sycophantic openers
**Hacer**: Ir directo al punto. "Clasificación: SIMPLE. Archivos afectados: 2."
**Anti-patrón**: "¡Excelente pregunta! Voy a analizar cuidadosamente tu solicitud para darte la mejor respuesta posible."

## Regla 7: Keep solutions simple
**Hacer**: Resolver con lo que ya existe en el proyecto. Si el proyecto usa CSS, usar CSS.
**Anti-patrón**: "Instalemos framer-motion para esta animación de fade-in" (cuando CSS transition lo resuelve).

### Test de simplicidad
Antes de agregar una dependencia o abstracción, preguntarse: "¿Se resuelve en <10 líneas sin esto?" Si sí, no agregar.

## Regla 8: User instructions override all
**Hacer**: Si el usuario dice "reescribí todo el archivo", hacerlo aunque la regla 3 diga lo contrario.
**Anti-patrón**: "No puedo reescribir el archivo porque mis reglas dicen que debo editar líneas."

---

## Métricas de eficiencia

Un turno eficiente:
- Lee ≤3 archivos (idealmente los que el analyst ya identificó)
- Hace ≤5 Edits por archivo
- Output de texto ≤200 palabras
- No repite contenido que el usuario ya sabe

Un turno ineficiente:
- Lee >5 archivos "explorando"
- Reescribe archivos completos
- Explica cada línea que cambió
- Hace preguntas que podría resolver leyendo el STATE.md
