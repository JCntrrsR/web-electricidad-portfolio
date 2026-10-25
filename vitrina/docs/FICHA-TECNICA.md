# Ficha técnica

## Stack

| Capa | Tecnología | Por qué |
|---|---|---|
| Framework | **React 18 + Vite** | interfaz reactiva y compilación rápida; agrupa por ruta |
| Lenguaje | **TypeScript** | los datos de negocio (cotización, agenda) no admiten tipos sueltos |
| Estilos | **Tailwind CSS** | sistema de diseño consistente sin CSS disperso |
| Rutas | **React Router 7** | rutas anidadas y carga diferida por página |
| Formularios | **React Hook Form + esquemas** | validación declarativa y errores por campo |
| Animación | **Framer Motion** | transiciones por composición, sin repintar layout |
| Auth y datos | **Supabase** | autenticación y base de datos sin backend propio |
| Pagos | **Stripe** | cobro con tarjeta y webhooks |
| Datos remotos | **TanStack Query** | caché, reintentos y estados de carga explícitos |
| PWA | **vite-plugin-pwa** | instalable y con soporte sin conexión |

## Tamaño del proyecto

| Métrica | Valor |
|---|---|
| Archivos en `src/` | 67 (51 `.tsx` · 15 `.ts`) |
| Líneas de código | ~13.300 |
| Dependencias de producción | 24 |
| Módulos de componente | 20+ |
| Migraciones de base de datos | 2 |
| Rutas | 12 |

## Módulos principales

| Módulo | Peso aproximado | Función |
|---|---|---|
| `BudgetCalculator` | 26 KB | motor de estimación con desglose |
| `seoOptimization` | 24 KB | metadatos y datos estructurados por ruta |
| `deviceTesting` | 19 KB | utilidades de verificación por dispositivo |
| `config/seo` | 19 KB | definición de metadatos del sitio |
| `ProjectGallery` | 18 KB | galería con visor y filtros |
| `SocialProof` | 17 KB | testimonios, cifras y certificaciones |
| `AppointmentScheduler` | 16 KB | calendario y reserva de franjas |
| `ContactForm` / `LeadCapture` | 15 KB + 12 KB | captura validada de contactos |
| `config/stripe` | 12 KB | inicialización y degradación del cobro |

## Verificación

```
npm run build        →  2323 módulos · 38 archivos · 3,2 MB · sin placeholders en el bundle
npm run test         →  pruebas de calculadora y captura de leads
npm run test:e2e     →  recorridos completos en navegador
```

Comprobaciones automáticas del build: existen los assets referenciados por el `index.html` y el
bundle no contiene claves de ejemplo (`your-project.supabase.co`, `pk_test_...`).

## Límites conocidos

| Límite | Motivo |
|---|---|
| Sin backend activo | el escaparate no debe depender de servicios ni incurrir en costos |
| Pagos en modo simulado | sin claves publicables; el flujo queda preparado |
| Área de cliente demostrativa | requiere base de datos conectada |
| Chat sin modelo | la ventana responde en modo demostración |
| Analítica inactiva | el script de medición apunta a un dominio no desplegado |

## Qué demuestra al cliente

- Un flujo comercial completo: **llegar → entender → cotizar → agendar → pagar**.
- Arquitectura modular con datos separados de la vista.
- Degradación controlada: si falta un servicio externo, el sitio sigue en pie.
- Criterio de producto: precios como rango, no como promesa; mensajes que reducen reclamos.
