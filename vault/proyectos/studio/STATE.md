# DataCore Studio — Estado Activo

## Metadata
- **proyecto**: studio
- **repo**: repositorio privado
- **branch**: main
- **version**: desarrollo
- **ultima_sesion**: 2026-04-10

---

## Fase actual
Migración de sistema de composición visual: de templates rígidos (`imageTemplate`) a bloques dinámicos (`DCComposition`). Fix aplicado, pendiente validación.

## Última sesión
- **Fecha**: 2026-04-10
- **Qué se hizo**: Inicialización del workspace centralizado
- **Build**: ✅ (limpio en última sesión de desarrollo)

## Completado reciente
- Reescritos `handlePostWriterInstagram` y `handlePostWriterLinkedin` en handlers.ts
- Eliminado todo `imageTemplate` de prompts de generación
- `composition` ahora obligatorio en JSON de respuesta
- `DESIGN_CONTEXT` simplificado: removida sección TEMPLATES DISPONIBLES
- `extractContent` en page.tsx detecta `json.composition`
- `remotionPostProps` pasa `composition` a `mapPostToRemotionProps`
- Build limpio

## Pendientes
- [ ] Verificar que generación inicial produce composición por bloques (correr `npx next dev -p 3001`)
- [ ] Validar que el chat de edición de diseño también usa bloques
- [ ] Testear los 14 tipos de elemento del ELEMENT_REGISTRY
- [ ] Hay cambios sin commitear en múltiples archivos del Studio

## Archivos modificados (última sesión)
- `src/lib/agent/handlers.ts` — prompts de generación reescritos
- `src/app/studio/page.tsx` — extractContent actualizado
- `src/lib/agent/design-prompt.ts` — DESIGN_CONTEXT simplificado
- `src/remotion/mapAgentToProps.ts` — pasa composition

## NO tocar (protegidos)
- `src/remotion/compositions/DCCompositionRenderer.tsx` — renderer nuevo, funciona
- `src/remotion/components/elements/` — element renderers, estables
- `src/remotion/types/` — tipos DCComposition, definidos

## Decisiones recientes
- Migración completa de imageTemplate → composition. Los 6 templates legacy quedan deprecados.

## Dependencias cruzadas
- **portfolio**: Studio es proyecto real para mostrar en el portafolio

## Notas para la próxima sesión
CRÍTICO: los dos prompts (`handlers.ts` y `design-prompt.ts`) DEBEN estar sincronizados. Si solo se actualiza uno, el agente vuelve a producir templates rígidos. Verificar siempre ambos archivos al hacer cambios en el sistema de composición.
