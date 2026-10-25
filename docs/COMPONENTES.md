# Componentes del escaparate — inventario y criterio

> Estado al 2026-10-23 después de la reparación del build. 50 archivos `.tsx`; 12 no se usan y
> cada uno tiene aquí su motivo. La regla: **un componente se usa o se documenta**, no se deja
> suelto aparentando estar vivo.

## Reglas

1. **Sin backend accidental.** Todo lo que escribe datos pasa por un modo demostración explícito
   (formularios con `setTimeout`, auth con `supabaseConfigurado`).
2. **SSR de configuración.** `src/lib/supabase.ts` expone si hay credenciales; nunca se asume que
   las hay. El sitio debe cargar igual sin `.env`.
3. **Un componente, una responsabilidad.** Si dos hacen lo mismo (`TestimonialSection` vs
   `TestimonialCarousel`), se elige uno y el otro se documenta para eliminar.
4. **Nada de sourcemaps en el build público** (ver `vite.config.ts`).

## En uso

| Componente | Dónde | Función |
|---|---|---|
| `Navbar` · `Footer` · `ScrollProgress` · `ScrollToTop` | App | estructura y navegación |
| `ErrorBoundary` · `Toast` | App | resiliencia y avisos |
| `ChatWidget` · `WhatsAppIntegration` | App | contacto flotante |
| `OnboardingTour` · `ConversionOptimizer` · `PerformanceOptimizer` · `SEOOptimizer` | App | conversión, rendimiento, SEO |
| `ServiceWorkerManager` | App | PWA / offline |
| `HeroSection` · `ServiceCard` · `TestimonialCarousel` · `KpiCard` | `pages/Home` | bloques de la home |
| `AnimatedSection` | varias | entrada animada |
| `BudgetCalculator` | `pages/Calculator` | estimación de presupuesto |
| `AppointmentScheduler` | `pages/Appointments` | agendamiento (demo) |
| `ContactForm` · `LeadCapture` | `pages/Contact` | captación (demo) |
| `ProjectGallery` | `pages/Projects` | galería de obras |
| `SocialProof` | varias | prueba social |
| `AuthProvider` | App | contexto de sesión (degrada sin Supabase) |

## Sin uso (decisión pendiente)

| Componente | Motivo | Recomendación |
|---|---|---|
| `PaymentProcessor` | requiere Stripe real + backend | dejar para producción |
| `TechnicianTracking` | requiere Supabase Realtime | dejar para producción |
| `ClientDashboard` | movido a `src/_no-publicado/`; dependía de un `Dashboard` que la sanitización borró y de 7 subcomponentes inexistentes | reconstruir cuando exista backend |
| `LoginForm` · `RegisterForm` | las páginas `auth/*` implementan su propio formulario | eliminar (duplican) |
| `CTASection` · `ServiceGrid` · `TestimonialSection` | la home resuelve esos bloques inline | adoptar o eliminar |
| `ParallaxBanner` | la home usa otra sección de cabecera | eliminar |
| `NotificationSystem` | `react-hot-toast` cubre el caso | eliminar |
| `__tests__/*` | tests de componentes que la home ya no usa | reescribir sobre los componentes vigentes |

## Qué se tocó para que compile y se comporte bien

| Archivo | Cambio |
|---|---|
| `src/pages/auth/ResetPassword.tsx` | import partido en dos líneas (`CheckCirc` / `le`) → `CheckCircle` |
| `src/pages/auth/Register.tsx` | residuo `</b` al final del archivo, que rompía el parseo |
| `src/App.tsx` | ruta `/dashboard` y su import eliminados (el archivo no existía); Stripe vía `getStripe()` en vez de una clave `pk_test_...` falsa |
| `src/lib/supabase.ts` | `supabaseConfigurado` + cliente inerte sin credenciales |
| `src/hooks/useAuth.ts` | sin Supabase no consulta sesión (antes quedaba en `loading` para siempre) y las acciones de auth devuelven un mensaje de demostración |
| `src/pages/auth/{Login,Register}.tsx` | aviso visible de modo demostración |
| `vite.config.ts` | `sourcemap: false` (publicaba 4,7 MB de código fuente) y `fastRefresh` obsoleto eliminado |
| `scripts/verificar-build.mjs` | verificación post-build: assets, CSS y placeholders de configuración |
| `src/_no-publicado/` | dashboard preservado, fuera del bundle |

## Librerías declaradas

`react`, `react-router-dom`, `framer-motion`, `react-scroll-parallax`, `@tanstack/react-query`,
`lucide-react`, `react-hot-toast`, `react-helmet-async`, `react-datepicker`, `js-cookie`,
`@stripe/react-stripe-js`, `@stripe/stripe-js`, `@supabase/supabase-js`, `@vercel/analytics`,
`@hookform/resolvers`, `react-hook-form`, `zod`, `recharts`.

Todas se usan salvo las de Stripe/Supabase en tiempo de datos: se compilan, pero solo se activan
con credenciales.
