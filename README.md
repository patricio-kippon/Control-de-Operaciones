# Mesa de Operaciones — sitio en GitHub Pages

Tablero interno del pipeline de deuda estructurada. Es un solo archivo, `index.html`,
sin dependencias ni servidor: se abre igual desde GitHub Pages o desde el disco.

La página tiene cinco secciones, con botones arriba: **Resumen** (indicadores,
Term Sheet firmado con sus mandatos y pipeline por etapa), **Operaciones** (la tabla
completa, cada fila se abre para ver el detalle de todos los frentes), **Proveedores**
(concentración por administrador, despacho y fiduciario, con montos y qué operaciones
lleva cada uno), **Contratos** (matriz de contratos por operación, para ver de un
vistazo qué falta firmar) e **Histórico** (cerradas y canceladas).

Los datos vienen del Excel `Seguimiento_Operaciones_Deuda_Estructurada_1.xlsx`
(SharePoint → Kippon → Operación → Control de Operaciones) y viajan **cifrados**
dentro del HTML. La página pide una contraseña y descifra en el navegador de quien
la abre; en el código fuente publicado no hay ni un monto ni un nombre en claro.

## Publicar por primera vez

1. Crea el repositorio en github.com — nombre sugerido `mesa-operaciones`, visibilidad **Public**.
2. Desde la carpeta que contiene este README:

   ```bash
   git init -b main
   git add .
   git commit -m "Mesa de Operaciones"
   git remote add origin https://github.com/TU-USUARIO/mesa-operaciones.git
   git push -u origin main
   ```

3. En el repo: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. Al minuto queda en `https://TU-USUARIO.github.io/mesa-operaciones/`.

Sin terminal: en el repo vacío, **Add file → Upload files**, arrastra `index.html`,
`.nojekyll` y este README, y **Commit changes**. Luego el paso 3.

## Actualizar los datos

Cada vez que quieras refrescar el tablero, pídeme "actualiza el dashboard": leo el
Excel de SharePoint, regenero `index.html` y te lo paso. Entonces:

```bash
# reemplaza el index.html de esta carpeta por el nuevo, y luego:
git add index.html
git commit -m "Datos al 27 de agosto"
git push
```

La URL no cambia. GitHub tarda alrededor de un minuto en reconstruir el sitio; si
ves lo viejo, recarga con Ctrl+Shift+R.

Sin terminal: entra a `index.html` en GitHub, botón de editar → **Upload files** para
reemplazarlo, o borra el archivo y sube el nuevo.

## Contraseña

La contraseña está incrustada en el cifrado del archivo, no en un campo que se pueda
editar. Para cambiarla hay que regenerar `index.html`: dime la nueva y te mando el
archivo listo.

Quien la tenga ve todo el tablero. Al escribirla, el navegador la recuerda hasta que
se cierra la pestaña.

No escribas la contraseña en este README ni en ningún archivo del repositorio: el
repo es público y eso anularía el cifrado. Compártela por otro canal.

## Qué protege y qué no

El cifrado es AES-256-GCM con la llave derivada por PBKDF2-SHA256 (250 000 iteraciones).
Eso significa que el repositorio puede ser público sin exponer la información: sin la
contraseña, el bloque de datos es ruido. Lo que no evita es que alguien con la
contraseña la comparta, ni que un atacante decidido intente adivinarla por fuerza
bruta — por eso conviene una contraseña larga y no reutilizada, y avisarme para
regenerar el archivo si alguien deja el equipo.
