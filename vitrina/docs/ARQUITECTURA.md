# Arquitectura

> Documento de vitrina: explica **cómo está construido** el sitio sin publicar el código.
> El detalle de implementación se comparte bajo acuerdo.

## Decisión principal: SPA con carga por ruta

El sitio se construyó como **aplicación de una sola página** con React y Vite porque el negocio
necesita tres cosas que un sitio estático no da bien juntas:

1. **Calculadora y agenda interactivas** — el estado cambia mientras el usuario decide.
2. **Área de cliente** — contenido que depende de quién está autenticado.
3. **Pago en línea** — un flujo que no puede recargar la página en medio.

Para que la SPA no pese como una SPA, cada ruta se carga **en diferido**: el visitante descarga
la portada y solo después el código de la página que visita.

## Capas

```
┌──────────────────────────────────────────────────┐
│ Proveedores raíz                                 │
│ autenticación · animación · pagos · SEO          │
└───────────────────────┬──────────────────────────┘
                        │
┌───────────────────────▼──────────────────────────┐
│ Rutas y páginas (carga diferida)                 │
│ inicio · servicios · proyectos · calculadora ·   │
│ agenda · contacto · faq · cuenta                 │
└───────────────────────┬──────────────────────────┘
                        │
┌───────────────────────▼──────────────────────────┐
│ Componentes de dominio                           │
│ calculadora · agenda · galería · formularios     │
└───────────────────────┬──────────────────────────┘
                        │
┌───────────────────────▼──────────────────────────┐
│ Servicios y datos                                │
│ cliente de base de datos · pagos · validación    │
└──────────────────────────────────────────────────┘
```

## Decisiones que sostienen el proyecto

**Los proveedores van por fuera del enrutador, salvo uno.**
La autenticación consume el estado de navegación, así que se monta **dentro** del enrutador. Si se
declara por fuera, cualquier hook que lea la ruta actual falla y la aplicación entera cae en la
pantalla de error. Es el error más caro de este tipo de arquitectura y está documentado en el
código.

**Los datos no viven dentro de las páginas.**
Blog, servicios, proyectos y preguntas frecuentes se declaran como datos tipados. La página solo
los pinta. Cambiar contenido no obliga a tocar la vista y el listado y el detalle comparten una
sola fuente.

**La validación es un contrato, no una comprobación suelta.**
Los formularios se validan contra un esquema declarado. El mismo esquema valida en el navegador y
sirve de referencia para lo que espera el backend.

**Los pagos se degradan, no se rompen.**
Si no hay clave publicable configurada, el módulo de cobro se desactiva y el resto del sitio sigue
funcionando. Antes, una clave falsa hacía fallar la librería de pagos dentro del árbol de React y
tumbaba la aplicación completa.

**El correo y la base de datos son sustituibles.**
La capa de datos se aisló detrás de un cliente único. Cambiar de proveedor no obliga a reescribir
páginas: se cambia el adaptador.

## Flujo de una cotización

```
visitante → calculadora → estimación en pantalla
         → deja datos  → validación → confirmación
         → (opcional) agenda la visita
         → (opcional) paga el anticipo
```

Cada paso es independiente: si el usuario abandona en la agenda, la cotización ya quedó registrada.

## Rendimiento

| Medida | Valor |
|---|---|
| Fragmentos por ruta | 12 (una por página) |
| Peso del build | ~3,2 MB |
| Peticiones bloqueantes al abrir | HTML + CSS + un solo fragmento JS |
| Animaciones | por composición (transform/opacity), sin repintar layout |

## Construcción

```
npm run build   →  compila TypeScript, agrupa por ruta y verifica assets del index
npm run test    →  pruebas de componentes (calculadora y captura de leads)
npm run test:e2e→  recorridos completos en navegador real
```
