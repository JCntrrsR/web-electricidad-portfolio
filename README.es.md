# web-electricidad-portfolio (Plataforma ElectroServicios Pro)

Aplicación web moderna en React para una empresa de servicios eléctricos, enfocada en generación de leads, presentación de servicios, agendamiento de citas, estimación de presupuestos y funcionalidades del ciclo de vida del cliente (auth, pagos, analítica y notificaciones).

## Overview

**web-electricidad-portfolio** es una plataforma frontend orientada al negocio para un proveedor de servicios eléctricos en Santiago, Chile. Combina un sitio de marketing con capacidades operativas como agendamiento de visitas técnicas, cálculo de presupuesto, autenticación e integración de pagos.

El repositorio incluye:
- Una aplicación web **Vite + React + TypeScript**.
- Integración con **Supabase** para datos, autenticación y migraciones.
- Una **Edge Function de Stripe** para eventos de pagos y suscripciones.
- Configuración **PWA** para comportamiento offline e instalación.
- Módulos utilitarios para analítica, SEO, rendimiento, validación y conversión.

En la práctica, el software ayuda al negocio eléctrico a:
- Capturar y convertir visitantes en potenciales clientes.
- Entregar herramientas de preventa (calculadora, FAQ, páginas de servicios).
- Centralizar interacciones con clientes (contacto, citas, onboarding).
- Preparar flujos operativos (proyectos, facturas, notificaciones, suscripciones).

## Features

- Sitio de marketing multipágina (Inicio, Servicios, Proyectos, Nosotros, Contacto, Blog, FAQ).
- Calculadora de presupuesto para estimaciones rápidas.
- Agendador de citas para visitas técnicas.
- Flujo de autenticación (login, registro, recuperación de contraseña).
- Integración de pagos con Stripe (frontend + webhook handler).
- Integración con Supabase (cliente auth/datos + migraciones SQL).
- Soporte SEO con metadata por página y utilidades específicas.
- Configuración PWA con registro de service worker.
- Componentes de conversión y engagement:
  - Integración con WhatsApp
  - Chat widget
  - Tour de onboarding
  - Social proof/testimonios
- Mejoras de UX/UI:
  - Rutas con lazy loading
  - Error boundary
  - Barra de progreso de scroll y secciones animadas
- Configuración base de pruebas con Vitest + Testing Library.

## Tech Stack

### Frontend
- React 18
- TypeScript
- Vite
- React Router
- Tailwind CSS
- Framer Motion

### Datos / Integración Backend
- Supabase JS client
- Migraciones SQL de Supabase
- Supabase Edge Function (Deno) para webhooks de Stripe

### Pagos
- Stripe JS + React Stripe

### Tooling / Calidad
- ESLint
- Vitest + Testing Library
- PostCSS + Autoprefixer
- Plugin PWA de Vite

## Architecture

El proyecto sigue una arquitectura frontend-first con responsabilidades modulares:

- **Capa de routing** (`src/App.tsx`): Define rutas, providers globales y sistemas transversales de UI.
- **Capa de páginas** (`src/pages`): Vistas a nivel de ruta (marketing, auth, citas, calculadora, etc.).
- **Capa de componentes** (`src/components`): Bloques de UI reutilizables, widgets de negocio y features especializadas.
- **Capa de hooks** (`src/hooks`): Abstracciones de lógica con estado (auth, analítica, dashboard, etc.).
- **Capa de configuración/utilidades** (`src/config`, `src/utils`, `src/lib`): Stripe, SEO, validaciones, helpers y cliente Supabase.
- **Capa backend-adjacent** (`supabase`): Migraciones SQL y edge functions para pagos/webhooks.

### Tipo de proyecto y estado actual

- **Tipo:** Aplicación web (sitio de negocio + plataforma de soporte operativo).
- **Estado actual:** **MVP / desarrollo activo**.
  - El código ya tiene un conjunto amplio de funcionalidades e integraciones.
  - Existen señales de evolución en curso (por ejemplo, rutas y módulos backend aún consolidándose).

## Installation

### Requisitos previos
- Node.js 18+ (recomendado)
- npm 9+
- (Opcional) Supabase CLI
- (Opcional) Stripe CLI

### Pasos

1. Clonar el repositorio:
   ```bash
   git clone <tu-url-del-repo>
   cd web-electricidad-portfolio
   ```

2. Instalar dependencias:
   ```bash
   npm install
   ```

3. Crear archivo de variables de entorno:
   ```bash
   cp .env.example .env.local
   ```
   Si `.env.example` no existe aún, crea `.env.local` manualmente.

4. Agregar variables mínimas requeridas:
   ```env
   VITE_SUPABASE_URL=
   VITE_SUPABASE_ANON_KEY=
   VITE_STRIPE_PUBLISHABLE_KEY=
   VITE_APP_URL=
   ```

5. Levantar servidor de desarrollo:
   ```bash
   npm run dev
   ```

## Usage

- Abrir `http://localhost:5173` tras ejecutar `npm run dev`.
- Navegar por las páginas públicas para validar contenido y flujos de conversión.
- Usar calculadora y módulo de citas para probar flujos de captación.
- Para eventos de pago, configurar webhooks de Stripe y desplegar la edge function de Supabase.
- Para funcionalidades dependientes de base de datos, correr migraciones y configurar credenciales.

## Project Structure

```text
web-electricidad-portfolio/
├── public/                     # Assets estáticos y recursos de service worker
├── scripts/                    # Scripts de automatización/configuración
├── src/
│   ├── components/             # Componentes reutilizables de UI y features
│   ├── config/                 # Configuración SEO y Stripe
│   ├── hooks/                  # Hooks personalizados de React
│   ├── lib/                    # Clientes externos (Supabase)
│   ├── pages/                  # Páginas por ruta
│   ├── test/                   # Setup de testing
│   ├── types/                  # Definiciones de tipos
│   ├── utils/                  # Utilidades (analítica, validación, SEO, etc.)
│   ├── App.tsx                 # Router principal y providers
│   └── main.tsx                # Punto de entrada de la app
├── supabase/
│   ├── functions/              # Edge functions (Stripe webhooks)
│   └── migrations/             # Migraciones de esquema/datos
├── index.html
├── package.json
├── tailwind.config.js
├── vite.config.ts
└── vitest.config.ts
```

## Development

### Comandos frecuentes

```bash
npm run dev            # Inicia servidor local de desarrollo
npm run build          # Compila para producción
npm run preview        # Previsualiza build de producción localmente
npm run lint           # Ejecuta lint
npm run test           # Ejecuta tests unitarios/de componentes
npm run test:coverage  # Ejecuta tests con cobertura
```

### Comandos Supabase / Stripe

```bash
npm run db:migrate     # Aplica migraciones a Supabase
npm run db:reset       # Resetea BD local de Supabase
npm run db:types       # Genera tipos TypeScript desde la BD
npm run stripe:listen  # Reenvía eventos webhook de Stripe en local
```

### Flujo recomendado

1. Crear rama de feature.
2. Implementar cambios aislados en `src/components`, `src/pages` o `src/hooks`.
3. Ejecutar lint/tests/build.
4. Abrir PR con capturas para cambios visuales y notas técnicas claras.

## Roadmap

Posibles mejoras próximas:

- Implementar ruta/dashboard faltante y routing protegido por roles.
- Agregar pipeline de CI (lint, test, build y validaciones de migraciones).
- Fortalecer cobertura de pruebas para formularios críticos y pagos.
- Incorporar estrategia i18n (español/inglés) más allá de la documentación.
- Completar endpoints API referenciados por helpers de pago en frontend.
- Añadir observabilidad (tracking de errores, logging estructurado, presupuestos de performance).
- Publicar guía de contribución y estándares de código.

## License

Esto es personal y privado, creado y desarrollado por JootaCee.

## Author

Esto es personal y privado, creado y desarrollado por JootaCee.
