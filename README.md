[README.md](https://github.com/user-attachments/files/31226673/README.md)
# Assets de email - Status semanal

Logos de clientes usados en el header del email de status semanal
(skill `weekly-status-email`, Paso 4b).

Se sirven vía jsDelivr desde este repo. **El repo tiene que ser público**: jsDelivr no lee repos privados.

## Convención de nombres

```
logos/<cliente>-logo.png
```

Cliente en minúscula, sin acentos ni espacios, guión medio como separador.

## Assets actuales

| Cliente       | Archivo                     | Asset    | Render (ancho x alto) | Fondo  |
|---------------|-----------------------------|----------|-----------------------|--------|
| JAZMÍN CHEBAR | `jazmin-chebar-logo.png`    | 280x60   | 140 x 30              | Blanco |
| PSA           | `psa-logo.png`              | 120x120  | 60 x 60               | Blanco |
| REX           | `rex-logo.png`              | 120x120  | 60 x 60               | Blanco |
| ROSEN         | `rosen-logo.png`            | 280x72   | 140 x 36              | Blanco |
| SOMMIERCENTER | `sommiercenter-logo.png`    | 280x67   | 140 x 33              | #6900A2 |

## Reglas de los assets

1. **El asset va al doble del tamaño de render**, para que se vea nítido en pantallas de alta densidad.
2. **Cada logo se ajusta dentro de una caja común de 140x60 px de render** (280x120 de asset),
   respetando su proporción original. No se fuerza un ancho fijo: un wordmark de 5:1 y un
   isotipo de 1:1 necesitan tratamientos distintos o uno de los dos queda desproporcionado.
3. **Se recorta el espacio muerto** antes de escalar. Un logo con mucho padding alrededor
   termina viéndose diminuto dentro de su caja.
4. **Fondo opaco, nunca transparente.** En el modo oscuro de Gmail, un wordmark oscuro sobre
   fondo transparente desaparece. El fondo se elige según el color del logotipo:
   - Logotipo oscuro → fondo blanco
   - Logotipo claro (ej: SommierCenter, blanco + lima) → fondo oscuro de la marca (#6900A2)
5. Peso objetivo: **bajo 20 KB** por archivo.

## URLs de producción

Formato:

```
https://cdn.jsdelivr.net/gh/<USUARIO>/<REPO>@main/logos/<archivo>
```

## Reemplazar un logo

El caché de jsDelivr es agresivo: si reemplazás un archivo manteniendo el nombre,
puede tardar días en propagarse. Después de pushear, forzar el purge:

```bash
curl "https://purge.jsdelivr.net/gh/<USUARIO>/<REPO>@main/logos/<archivo>"
```

Verificar que la URL devuelva la imagen y no una página de GitHub:

```bash
curl -sI "https://cdn.jsdelivr.net/gh/<USUARIO>/<REPO>@main/logos/rex-logo.png" \
  | grep -i "http/\|content-type"
```

Esperado: `200` y `content-type: image/png`.

## Agregar un cliente nuevo

1. Conseguir el logo en el mayor tamaño disponible (PNG, SVG o WEBP; evitar capturas).
2. Recortar el espacio muerto, ajustar dentro de la caja de 280x120 y aplanar sobre el
   fondo que corresponda según el punto 4.
3. Guardar como `logos/<cliente>-logo.png` y pushear.
4. Cargar la URL, `LOGO_ANCHO` y `LOGO_ALTO` en la tabla de logos de la skill
   `weekly-status-email`.
