# AniVero

## Proyecto personal

Una plataforma **SaaS modular multi-tenant** para negocios locales, empezando por hostelería.

![AniVero — Flujo QR, pedido y pago seguro](./img/anivero.png)

El primer módulo, **`coffee-connect-table`**, resuelve un flujo completo: el cliente escanea un QR, consulta la carta, hace un pedido, paga desde el móvil y el local recibe un pedido numerado listo para preparar.

---

## Problema

Los negocios locales necesitan herramientas digitales simples, pero los SaaS del mercado suelen ser genéricos, caros o difíciles de adaptar. AniVero propone una plataforma modular donde cada negocio activa solo lo que necesita.

## Stack

- **Next.js + TypeScript** (frontend)
- **Supabase** (backend, Auth, Edge Functions)
- **PostgreSQL** con Row Level Security
- **Stripe Connect** (pagos)
- **Resend** (alertas)
- **pgTAP + Deno test** (testing)

## Testing

El proyecto se verifica con evidencia, no solo con revisión manual:

- **122 assertions pgTAP** sobre aislamiento de tenants, RLS, catálogo público e integridad de pedidos/pagos.
- **30 tests Deno** sobre las Edge Functions de pago y webhook.

## Estado actual

**Backend / MVP:** núcleo multi-tenant, catálogo público, pedidos anónimos, pagos e integridad, webhook de Stripe y suite de tests — completos.
