# Skill: Change Classifier

## Propósito
Criterio detallado para que el orchestrator clasifique la complejidad de un cambio.

---

## Nivel: MÍNIMO
**Flujo**: `developer` → `memory-keeper`

### Criterios (TODOS deben cumplirse)
- Afecta exactamente 1 archivo
- No toca lógica de negocio
- No cambia tipos/interfaces
- No afecta estado (Zustand, Context, BD)
- El cambio es mecánico, no requiere decisión

### Ejemplos
- Corregir un typo en texto visible
- Cambiar un color CSS
- Actualizar un string de traducción
- Ajustar padding/margin
- Cambiar un ícono de Lucide

---

## Nivel: SIMPLE
**Flujo**: `analyst` → `developer` → `memory-keeper`

### Criterios (al menos 1)
- Afecta 1-3 archivos
- Lógica contenida en un módulo (no cruza boundaries)
- Sin dependencias cruzadas con otros componentes
- No toca BD ni auth

### Ejemplos
- Agregar un campo a un formulario (componente + validación)
- Crear un componente nuevo simple
- Modificar un endpoint existente (mismos parámetros)
- Agregar una key de traducción con su uso
- Cambiar el orden de secciones en una página

---

## Nivel: COMPLEJO
**Flujo**: `analyst` → `developer` → `auditor` → `tester` → `memory-keeper`

### Criterios (al menos 1)
- Afecta 4+ archivos
- Toca modelos de datos o tipos compartidos
- Modifica rutas o navegación
- Cambia estado global (Zustand store, Context providers)
- Tiene dependencias cruzadas entre componentes
- Requiere migración de datos (no de schema)

### Ejemplos
- Agregar un módulo nuevo con ruta, componente y API
- Refactorear un flujo existente (ej: checkout)
- Integrar un servicio externo
- Agregar un filtro complejo con estado persistente
- Cambiar la estructura de navegación

---

## Nivel: CRÍTICO
**Flujo**: `analyst` → `developer` → `auditor` → `tester` → `memory-keeper` + decisión en vault

### Criterios (al menos 1)
- Afecta schema de BD (nuevas tablas, columnas, índices)
- Toca auth, permisos o RLS
- Modifica flujos de pago o datos financieros
- Afecta múltiples proyectos simultáneamente
- Cambia arquitectura (nuevo provider, nuevo patrón de estado)
- Es irreversible o muy costoso de revertir

### Ejemplos
- Sistema de sucursales (multi-branch)
- Facturación electrónica
- Cambio de sistema de auth
- Migración de base de datos con transformación
- Nuevo sistema de roles/permisos
- Integración con API de pagos

---

## Decisión rápida

```
¿Toca BD/auth/seguridad? → CRÍTICO
¿4+ archivos o estado global? → COMPLEJO
¿2-3 archivos con lógica? → SIMPLE
¿1 archivo sin lógica? → MÍNIMO
```

En caso de duda, clasificar un nivel más alto. Es más barato auditar de más que debugear un bug en producción.
