# AniVero

## Plataforma SaaS multi-tenant para hostelería

AniVero es una plataforma de software diseñada para digitalizar y simplificar la gestión de establecimientos de hostelería.

Integra una **carta digital multidioma**, un panel de gestión para cada negocio y un módulo configurable de **pedidos desde la mesa, pagos e impresión de comandas**.

Su arquitectura modular permite adaptar las funcionalidades a las necesidades operativas de cada establecimiento.

![AniVero — Carta digital y gestión de pedidos](./img/centro-control-anivero.webp)

**[Probar la demostración](https://www.anivero.es/m/demo)** · **[Ver caso de proyecto](./CASO-DE-PROYECTO.md)** · **[Recorrido visual (PDF)](./AniVero_carrusel.pdf)**

> La demostración pública utiliza datos de ejemplo y permite completar un pedido simulado. No procesa pagos ni envía pedidos reales. Sus limitaciones no representan las capacidades completas de la plataforma.

---

## Funcionalidades

### Carta digital

Implementada y operativa en producción.

- Carta independiente por establecimiento, accesible mediante URL, subdominio o código QR.
- Cinco idiomas: español, inglés, francés, portugués y alemán.
- Información estructurada de los 14 alérgenos del Reglamento (UE) 1169/2011.
- Categorías, fotografías, vídeos y formatos de precio por producto.
- Identidad visual y banners promocionales configurables.
- Disponibilidad de productos y contenido administrable.

### Gestión del establecimiento

Panel `/gestion` para que cada negocio administre su carta:

- Crear, editar, ordenar y retirar productos y categorías.
- Gestionar disponibilidad, precios y alérgenos.
- Administrar imágenes, idiomas y traducciones.
- Configurar funcionalidades habilitadas para el establecimiento.

La plataforma dispone de un Dashboard Maestro para administrar locales, identidades y capacidades, importar cartas mediante CSV y gestionar la configuración general. El acceso administrativo está protegido mediante MFA.

### MesaPide — Pedidos desde la mesa

Módulo desarrollado para gestionar el recorrido desde la selección del pedido hasta la impresión de la comanda:

- Identificación de la mesa mediante un token seguro asociado al QR.
- Selección de productos y revisión del pedido.
- Métodos de pago configurables por establecimiento.
- Control para activar o desactivar el servicio.
- Generación e impresión de comandas mediante un agente local para Windows desarrollado en Go.

**Validación:** el circuito de pedidos en efectivo e impresión se ha probado en producción en un local de prueba.

Su activación comercial requiere configurar las mesas, los dispositivos y la operativa del establecimiento.

### Pagos online

Integración desarrollada con **Stripe Connect**:

- Cobros directos en la cuenta conectada del establecimiento.
- Importe recalculado en el servidor.
- Idempotencia para evitar operaciones duplicadas.
- Confirmación de pagos mediante webhooks.

La integración cuenta con pruebas automatizadas y validación en sandbox.

**No se acredita todavía un cobro real con tarjeta en producción.** Su activación requiere el acuerdo con el empresario, una cuenta Stripe conectada y la configuración correspondiente.

---

## Arquitectura tecnológica

| Componente            | Tecnología                        |
| --------------------- | --------------------------------- |
| Frontend              | Next.js 15, React 19, TypeScript  |
| Interfaz              | Tailwind CSS 4                    |
| Backend               | Supabase, PostgreSQL 17           |
| Autenticación         | Supabase Auth                     |
| Seguridad de datos    | Row Level Security (RLS)          |
| Funciones de servidor | Supabase Edge Functions (Deno)    |
| Pagos                 | Stripe Connect                    |
| Impresión             | Agente Windows desarrollado en Go |
| Notificaciones        | Resend                            |
| Despliegue web        | Vercel                            |

### Arquitectura multi-tenant

AniVero utiliza una base de datos compartida con aislamiento lógico entre establecimientos.

La identificación del local activo se integra en la autenticación mediante JWT, y el acceso a los datos se controla con políticas RLS y funciones de base de datos con privilegios acotados.

Las operaciones sensibles, como pedidos, permisos y pagos, se validan en el servidor.

---

## Calidad y validación técnica

El proyecto incorpora pruebas automatizadas de base de datos, backend e interfaz.

Según el informe técnico de `main` del 18/11/2026:

- **69 migraciones** de base de datos.
- **1.023 comprobaciones pgTAP** declaradas para contratos, permisos, integridad y aislamiento entre establecimientos.
- **122 tests Deno** para funciones de servidor.
- **Aproximadamente 1.811 casos Vitest** para la aplicación web.
- **Pruebas end-to-end con Playwright**, incluyendo regresión visual de la carta digital.

Las pruebas forman parte de los workflows de GitHub Actions. El último commit examinado en el informe tenía las comprobaciones de backend, frontend y carta visual superadas.

Las cifras corresponden a los casos declarados en el repositorio en esa revisión.

---

## Estado del proyecto

**Carta digital:** operativa en producción, con gestión independiente por establecimiento.

**Panel de administración:** implementado y operativo.

**MesaPide:** circuito funcional validado con pedidos en efectivo e impresión en un local de prueba. Pendiente de configuración para cada nueva implantación.

**Pagos con tarjeta:** integración implementada y probada en sandbox; pendiente de activación y validación comercial.

### Próximos pasos operativos

- Activación del acceso por invitación para nuevos propietarios.
- Herramientas de administración de mesas y códigos QR.
- Despliegue de la expiración automática de pedidos pendientes.
- Finalización de los enlaces legales de la carta.
- Mejoras de observabilidad y automatización de copias de seguridad.

La comercialización se plantea por fases, comenzando por la carta digital y su panel de gestión.

---

## Caso de proyecto

El recorrido funcional de la demostración está documentado con capturas reales:

**[Consultar caso de proyecto](./CASO-DE-PROYECTO.md)**

**[Abrir demostración interactiva](https://www.anivero.es/m/demo)**

---

**AniVero** · Proyecto personal de Anibal Solano.
