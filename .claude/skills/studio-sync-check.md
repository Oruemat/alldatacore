# Skill: Studio Sync Check

## Propósito
Verificación automática de que los dos prompts paralelos de Studio (`handlers.ts` y `design-prompt.ts`) están sincronizados. El auditor la aplica cuando el scope del cambio toca el sistema de composición.

## Cuándo se aplica
- El developer tocó `src/lib/agent/handlers.ts` o `src/lib/agent/design-prompt.ts`
- El developer tocó `ELEMENT_REGISTRY` o cualquier archivo en `src/remotion/types/` que define el schema `DCComposition`
- El change-classifier marcó el cambio como CRÍTICO por prompts paralelos

---

## Checklist obligatorio

### 1. Ambos archivos fueron modificados
```
✅ Edit aplicado a src/lib/agent/handlers.ts
✅ Edit aplicado a src/lib/agent/design-prompt.ts
```
Si solo hay uno → ❌ **FALLA**. El developer debe completar el par antes de continuar.

### 2. El campo `composition` es obligatorio en ambos
Buscar en cada archivo:
```
Grep: "composition" en el prompt
Grep: "imageTemplate" NO debe aparecer como campo requerido
```

### 3. El JSON schema pedido al LLM es equivalente
Los dos prompts piden al modelo un JSON con la misma estructura. Verificar:
- Mismo nombre de campo raíz (`composition`)
- Misma descripción del contenido esperado (bloques dinámicos, no templates rígidos)
- Misma lista de tipos de elemento permitidos (coincide con `ELEMENT_REGISTRY`)

### 4. `extractContent` detecta el output
En `src/app/studio/page.tsx`:
```
Grep: "json.composition" → debe existir
Grep: "json.imageTemplate" → NO debe existir como path requerido
```

### 5. `mapAgentToProps` propaga composition
En `src/remotion/mapAgentToProps.ts`:
```
Grep: "composition" como prop pasado a mapPostToRemotionProps
```

### 6. Tipos sincronizados
Si se modificó `ELEMENT_REGISTRY` o los tipos en `src/remotion/types/`:
- Cada tipo nuevo debe estar listado en ambos prompts
- Cada tipo removido debe desaparecer de ambos prompts

---

## Output del auditor

```markdown
## Studio Sync Check

### Archivos verificados
- src/lib/agent/handlers.ts — modificado: [SÍ/NO]
- src/lib/agent/design-prompt.ts — modificado: [SÍ/NO]
- src/app/studio/page.tsx — extractContent detecta composition: [SÍ/NO]
- src/remotion/mapAgentToProps.ts — propaga composition: [SÍ/NO]

### Schema check
- composition es obligatorio en ambos prompts: [SÍ/NO]
- imageTemplate removido de ambos prompts: [SÍ/NO]
- Tipos de ELEMENT_REGISTRY alineados: [SÍ/NO]

### Veredicto
- ✅ PROMPTS SINCRONIZADOS — approve
- ❌ DESINCRONIZADOS — requiere fix en: [archivo específico]
```

---

## Por qué esta skill existe

Ya ocurrió el bug: se actualizó uno de los dos prompts y el agente volvió a producir `imageTemplate` rígido en vez de `composition`. La única forma de detectarlo rápido es esta verificación cruzada. Sin ella, el bug aparece en producción al generar un post.
