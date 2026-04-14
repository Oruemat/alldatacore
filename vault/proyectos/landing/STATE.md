# DataCore Landing — Estado Activo

## Metadata
- **proyecto**: landing
- **repo**: https://github.com/Oruemat/landing-datacore
- **branch**: main
- **version**: producción
- **ultima_sesion**: 2026-04-10

---

## Fase actual
Landing en producción. Pendiente conectar dominio y configurar flujo de demo requests para POS.

## Última sesión
- **Fecha**: 2026-04-10
- **Qué se hizo**: Inicialización del workspace centralizado
- **Build**: ✅

## Completado reciente
- Hero, Beneficios, Sobre Nosotros, Portafolio, Contacto funcionales
- Página POS con modal de demo request
- Navbar con dropdown Productos → Sistema POS
- SEO completo, favicon, Edge Function de email contacto
- Formulario de contacto general con notificación por email

## Pendientes
- [ ] Crear tabla `demo_requests` en Supabase con RLS (INSERT policy para `anon`)
- [ ] Deploy Edge Function `send-demo-request` a Supabase
- [ ] Configurar secrets (GMAIL_USER, GMAIL_APP_PASSWORD, NOTIFY_EMAIL)
- [ ] Crear Database Webhook on INSERT a `demo_requests`
- [ ] Conectar dominio www.datacore.com.py a Vercel

## Archivos modificados (última sesión)
- Ninguno — sesión de setup del workspace

## NO tocar (protegidos)
- `src/components/Contact.tsx` — formulario de contacto funcional en producción
- Edge Function `send-contact-email` — funciona correctamente

## Decisiones recientes
- Ninguna reciente

## Dependencias cruzadas
- **pos**: La página `/pos` es la vitrina del Sistema de Gestión
- **portfolio**: La landing es proyecto real para mostrar en el portafolio

## Notas para la próxima sesión
Los commits recientes están documentados en el CLAUDE.md del proyecto. El flujo de contacto general ya funciona; falta replicar el mismo patrón para demo_requests.
