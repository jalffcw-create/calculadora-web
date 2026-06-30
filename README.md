# Calculadora web

Una calculadora básica con interfaz gráfica que funciona en el navegador. Sin dependencias: es un único archivo HTML.

## Uso

Ábrela online en **https://jalffcw-create.github.io/calculadora-web/**

O abre `index.html` en cualquier navegador (doble clic) o:

```bash
open index.html
```

## Funciones

- Operaciones: suma, resta, multiplicación, división y porcentaje
- `C` borra todo, `⌫` borra el último carácter
- Soporte de teclado: números y operadores, `Enter` para calcular, `Backspace` para borrar, `Esc` para limpiar
- Manejo de errores (división entre cero y expresiones inválidas)
- **Historial en la nube**: cada cálculo se guarda en una base de datos PostgreSQL (Supabase) y se muestra en el panel de la derecha, compartido entre dispositivos. Haz clic en un cálculo para reutilizar su resultado.

## Base de datos

El historial usa [Supabase](https://supabase.com). La tabla se crea con:

```sql
create table historial (
  id bigint generated always as identity primary key,
  expresion text not null,
  resultado text not null,
  creado_en timestamptz default now()
);
alter table historial enable row level security;
create policy "acceso publico" on historial for all using (true) with check (true);
```

La URL del proyecto y la *publishable key* van en `index.html` (la publishable key es segura para el navegador con RLS activado).
