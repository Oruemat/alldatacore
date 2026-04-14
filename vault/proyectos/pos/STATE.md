# Sistema de Gestión (POS) — Estado Activo

## Metadata
- **proyecto**: pos
- **repo**: https://github.com/Oruemat/sistema_gestion
- **branch**: main
- **version**: v1.2.2
- **ultima_sesion**: 2026-04-10

---

## Fase actual
v1.2.2 en producción. Sistema de sucursales completo. Próxima versión planificada: v2.0.0 (Facturación Electrónica).

## Última sesión
- **Fecha**: 2026-04-10
- **Qué se hizo**: Inicialización del workspace centralizado
- **Build**: ✅

## Completado reciente (v1.2.x)
- Sistema de sucursales multi-branch completo
- BranchContext: owner carga todas las sucursales
- BranchSelector dropdown en Sidebar y MobileHeader
- BranchManagement CRUD para owners
- Inventario por sucursal con branch_stock
- Manual de usuario v1.2 con sección Sucursales
- Owner multi-branch navigation

## Versiones completadas
v0.0.x → v1.2.2 todas en main ✅

## Pendientes
- [ ] v2.0.0: Facturación Electrónica (Billpy/SIFEN)
- [ ] Evaluar requerimientos SIFEN para Paraguay
- [ ] Integración con API Billpy

## Archivos modificados (última sesión)
- Ninguno — sesión de setup

## NO tocar (protegidos)
- `supabase/migrations/` — migraciones aplicadas en producción
- `contexts/AuthContext.tsx` — sistema de auth/RBAC estable
- `contexts/BranchContext.tsx` — multi-branch estable
- `lib/rbac.ts` — permisos validados

## Decisiones recientes
- v1.2.0: Stock independiente por sucursal (branch_stock), catálogo compartido por empresa
- v1.2.0: products.stock como cache agregado via trigger
- v1.2.0: Numeración con prefijo sucursal: SUC01-YYYYMMDD-NNNN

## Dependencias cruzadas
- **landing**: La página `/pos` en la landing es la vitrina del sistema
- **portfolio**: El POS es el proyecto más complejo para mostrar
- Supabase project compartido con landing: `tkgcacbjndmsgxngmtmt`

## Notas para la próxima sesión
El sistema es multi-tenant con RBAC completo. Cualquier cambio que toque BD debe considerar: RLS por company_id, branch_id NOT NULL en tablas operacionales, y el trigger de sync de stock. Las migraciones nuevas deben ejecutarse en Supabase Cloud ANTES del push.
