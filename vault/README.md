# DataCore Vault — Obsidian

Este vault es la memoria persistente de Claude entre sesiones.

## Estructura

```
vault/
├── proyectos/           ← Estado activo de cada proyecto
│   ├── landing/STATE.md
│   ├── studio/STATE.md
│   ├── workspace/STATE.md
│   ├── pos/STATE.md
│   └── portfolio/STATE.md
├── decisiones/          ← Decisiones arquitecturales (ADRs)
│   └── (YYYY-MM-DD-slug.md)
├── diario/              ← Resumen de cada sesión
│   └── (YYYY-MM-DD.md)
├── conceptos/           ← Patrones y convenciones reutilizables
│   └── (nombre.md)
└── templates/           ← Templates base
    ├── STATE-template.md
    ├── diario-template.md
    ├── decision-template.md
    └── session-prompts.md
```

## Reglas

1. **Solo el memory-keeper escribe en el vault** — otros agentes leen
2. **STATE.md es la fuente de verdad** — Claude lee esto al iniciar
3. **Diario solo para sesiones significativas** — no para typos
4. **Decisiones solo para cambios que afectan arquitectura** — no para CSS
5. **Conceptos son cross-project** — patrones que aplican a más de un proyecto

## Convenciones de nombrado
- Decisiones: `YYYY-MM-DD-slug-descriptivo.md`
- Diario: `YYYY-MM-DD.md`
- Conceptos: `nombre-descriptivo.md` (kebab-case)
