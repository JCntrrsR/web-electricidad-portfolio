# Funcionalidades

> Qué hace el sitio, módulo por módulo. Cada bloque indica **para quién existe**, no solo qué pinta.

## 1. Portada

**Para qué:** que en pocos segundos se entienda qué ofrece la empresa, dónde opera y qué hacer a
continuación.

**Incluye:** propuesta de valor, motivos para elegirla, resumen de servicios, proyectos destacados,
cifras de respaldo, certificaciones, testimonios, comparación de planes y preguntas frecuentes.

## 2. Servicios

**Para qué:** que el cliente identifique su problema sin leer un catálogo técnico.

**Incluye:** cinco servicios con descripción, alcance y llamada a la acción propia. Cada tarjeta
lleva a la cotización con el servicio ya preseleccionado.

## 3. Proyectos y galería

**Para qué:** dar evidencia visual. Un cliente contrata obra, no texto.

**Incluye:** cuadrícula filtrable por tipo de trabajo, visor ampliado con navegación y ficha de cada
proyecto (tipo, superficie, plazo, servicios ejecutados).

## 4. Calculadora de presupuesto

**Para qué:** eliminar la principal objeción —«no sé cuánto costará»— sin esperar una llamada.

**Incluye:** selección de tipo de trabajo, superficie o cantidad, extras y urgencia. Devuelve un
rango estimado con desglose y ofrece convertir la estimación en solicitud de visita.

**Decisión:** el resultado es un **rango**, no un precio cerrado. Un presupuesto exacto requiere
inspección y prometerlo por adelantado genera reclamos.

## 5. Agenda de visitas

**Para qué:** capturar al cliente que ya decidió, en el momento en que decidió.

**Incluye:** calendario con fechas disponibles, selección de franja horaria, datos de contacto y
confirmación. Validación por pasos para no pedir todo de golpe.

## 6. Contacto

**Para qué:** canal para quien prefiere escribir antes que agendar.

**Incluye:** formulario validado, canales directos (teléfono, WhatsApp, correo), mapa de ubicación
y horario de atención.

## 7. Preguntas frecuentes

**Para qué:** reducir consultas repetidas y objeciones de último minuto (plazos, garantías, pagos,
cobertura).

**Incluye:** acordeón por tema con respuesta redactada para lectura rápida, no para lucirse.

## 8. Cuenta de cliente

**Para qué:** que quien ya contrató pueda volver sin empezar de cero.

**Incluye:** registro, inicio de sesión, recuperación de contraseña y panel con sus solicitudes.

**Estado en la vitrina:** la interfaz funciona; la autenticación real requiere backend conectado.

## 9. Canales de contacto flotantes

**Para qué:** que el cliente no tenga que buscar cómo escribir.

**Incluye:** botón de WhatsApp persistente y ventana de conversación. En la vitrina el chat responde
en modo demostración.

## 10. Transversales

| Capacidad | Detalle |
|---|---|
| **SEO** | título, descripción y datos estructurados por ruta; sitemap |
| **PWA** | instalable, con soporte sin conexión y aviso de actualización |
| **Accesibilidad** | foco visible, contraste, textos alternativos, navegación por teclado |
| **Analítica** | eventos de conversión: cotización calculada, visita agendada, formulario enviado |
| **Rendimiento** | carga diferida por ruta y animaciones sin repintado |
| **Errores** | pantalla de recuperación en lugar de página en blanco |

## Lo que la vitrina **no** hace

- No envía correos ni guarda datos: los formularios confirman en pantalla.
- No cobra: el flujo de pago está preparado y desactivado sin claves.
- No autentica de verdad: el área de cliente es navegable en modo demostración.
