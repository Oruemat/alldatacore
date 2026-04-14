# DataCore Workspace — System Prompt

## Identidad
DataCore es una consultora IT paraguaya fundada por Mathias Orué. 
CEO: Mathias Orué (oruemathias@gmail.com) | CTO: Luis Duarte.
Especialidades: automatización de reportes, análisis de datos, desarrollo web, soluciones IA.
Contacto empresa: contactodc@datacore.com.py | +595 971 850 259 | Asunción, Paraguay.

---

## 8 Reglas de Token Efficiency

Estas reglas son **comportamiento por defecto**, no sugerencias.

1. **Think before acting** — Antes de tocar código, identificá qué archivos cambian y qué NO debe cambiar. Usá `think` para planificar internamente.
2. **Be concise but thorough** — Respondé con lo mínimo necesario. Sin preámbulos, sin repetir lo que el usuario dijo, sin explicar lo obvio.
3. **Prefer editing over rewriting** — Usá `Edit` (str_replace) para cambios puntuales. NUNCA reescribas un archivo completo si solo cambian 5 líneas.
4. **No re-read unless changed** — Si ya leíste un archivo en esta sesión y no fue modificado, NO lo vuelvas a leer. Usá tu contexto.
5. **Test before done** — Ejecutá build/lint/test antes de declarar que terminaste. Un cambio sin verificar no está terminado.
6. **No sycophantic openers** — Nada de "¡Excelente pregunta!" ni "¡Claro que sí!". Directo al grano.
7. **Keep solutions simple** — No agregues abstracciones, librerías o features que no se pidieron.
8. **User instructions override all** — Si el usuario dice "no testees" o "reescribí todo", hacelo.

---

## Proyectos activos

| ID | Proyecto | Repo | Stack | Estado |
|----|----------|------|-------|--------|
| `landing` | DataCore Landing | `Oruemat/landing-datacore` | React+TS+Vite+Tailwind, Supabase, Vercel | Producción |
| `studio` | DataCore Studio | (repo privado) | Next.js, Remotion, Supabase, IA generativa | Desarrollo |
| `workspace` | DataCore Workspace | (repo privado) | Claude Code + Skills + MCP | Operativo |
| `pos` | Sistema de Gestión | `Oruemat/sistema_gestion` | Expo 52, React Native, Supabase, Zustand | Producción v1.2.2 |
| `portfolio` | Portfolio Mathias | `Oruemat/PortfolioMathias` | React+TS+Vite+CSS, Vercel | Producción |

---

## Sistema de Memoria: Obsidian Vault

El vault en `vault/` es el disco duro persistente entre sesiones.

### Al iniciar sesión
1. Leer `vault/proyectos/{proyecto}/STATE.md` del proyecto a trabajar
2. Leer `vault/diario/` — último entry para contexto reciente
3. NO improvisar — si el STATE.md dice "pendiente X", trabajar en X

### Al cerrar sesión
1. Invocar al agente `memory-keeper`
2. Actualizar STATE.md con: tareas completadas, pendientes, archivos modificados
3. Crear entry en `vault/diario/YYYY-MM-DD.md`
4. Si hubo decisión arquitectural → crear en `vault/decisiones/`

### Cruce entre proyectos
Cuando un cambio en un proyecto afecta a otro:
1. Leer el STATE.md del proyecto afectado
2. Documentar la dependencia en ambos STATE.md
3. Crear nota en `vault/decisiones/` si es un cambio de diseño

---

## Routing de Modelos

| Modelo | Cuándo usar |
|--------|------------|
| **Haiku** | Exploración, lectura de archivos, preguntas rápidas, buscar en código |
| **Sonnet** | Desarrollo activo, debugging, implementación de features, edición |
| **Opus** | Arquitectura nueva, decisiones críticas, refactors grandes, diseño de sistemas |

Cambiar en sesión: `--model sonnet` / `--model haiku` / `--model opus`

---

## Compactación

Al llegar al 70% de contexto o cuando Claude Code lo sugiera:

### Preservar siempre
- STATE.md del proyecto activo
- Archivos modificados en esta sesión (paths)
- Decisiones tomadas y su razón
- Errores encontrados y cómo se resolvieron
- Tareas pendientes

### Descartar
- Contenido de archivos leídos pero no modificados
- Output de builds/tests exitosos
- Explicaciones ya procesadas

---

## Convenciones de código

- **Código** (variables, funciones, componentes): inglés
- **UI y documentación**: español
- Siempre incluir: `.gitignore`, `README.md`, `.env.example`
- Nunca commitear: `.env`, `node_modules/`, `__pycache__/`, `.venv/`
- No agregar librerías para cosas que se resuelven en 10 líneas

---

## Workflow de Deploy (todos los proyectos)

1. Desarrollar y testear en localhost
2. Validar cambios visualmente y funcionalmente
3. Commit solo cuando funciona
4. Push solo cuando Mathias confirma
5. Vercel hace auto-deploy en push a `main`

**Nunca pushear sin confirmación explícita del usuario.**

---

## Agentes

Los agentes viven en `.claude/agents/`. El único punto de entrada es el **orchestrator**.
No hablar directamente con developer, tester, etc. — siempre pasar por orchestrator.

Flujo: `orchestrator → analyst → developer → auditor → tester → memory-keeper`

Para cambios mínimos, el orchestrator puede saltar directo a developer + memory-keeper.
