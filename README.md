# Instalaciones Egondo · nueva web (prototipo)

Prototipo de la nueva web de **Instalaciones y Montajes Eléctricos Egondo, S.A.** (Ermua, Bizkaia), hoy en instalacionesegondo.com.

Está hecha en HTML, CSS y JavaScript planos: sin Node, sin compilación y sin dependencias. Se sube tal cual a cualquier hosting (FTP, Cloudflare Pages, Netlify, GitHub Pages…).

Todos los datos (servicios, autorizaciones, historia, dirección, horario) salen de la web actual. Lo que no estaba ahí aparece marcado en amarillo como `[dato a confirmar]`.

## Verla

Abrir `index.html` con doble clic. Las rutas son relativas, así que funciona igual en local y en el hosting:
- **Enlaces:** con doble clic (`file://`), `js/app.js` hace que los enlaces a carpetas abran su `index.html`.
- **Fuente:** en ese caso el navegador bloquea las fuentes web, así que se carga `fonts/saira-egondo.js`, que lleva la fuente incrustada.

En el hosting no hace falta ninguno de los dos ajustes.

`404.html` usa rutas absolutas porque el servidor la muestra en cualquier URL. Para verla en local: `python3 -m http.server 8000`.

## Sistema de diseño

| | |
|---|---|
| Azul Egondo | `#082088`: barra superior, sección «Empresa», pie y acentos de texto |
| Amarillo Egondo | `#F8D808`: solo para la acción principal (botón de llamar y presupuesto), con texto azul |
| Verde Egondo | `#007830`: solo en el logotipo |
| Neutros | tinta `#0E1424`, gris `#464D5C`, papel `#F3F5F9`, filetes `#DFE3EA` |
| Tipografía | Saira (variable, licencia OFL), autoalojada en `fonts/` y recortada a 52 KB. Titulares condensados en mayúsculas |
| Logotipo | Redibujado en SVG a partir del PNG de la web actual. **Sustituir por el vector original** si el cliente lo tiene |
| Lenguaje gráfico | Filetes en lugar de tarjetas y láminas técnicas en SVG (esquema unifilar y alzado de un centro de transformación) en lugar de imágenes de stock |

Los colores están definidos como variables al principio de `css/estilos.css`.

## Estructura

```
index.html                                     Home
mantenimiento-centros-transformacion/          Landing modelo (SEO + Google Ads, sin menú)
contacto/                                      Contacto y cómo llegar
eu/                                            Versión en euskera (estructura; textos por validar)
aviso-legal/  privacidad/                      Plantillas legales (noindex)
404.html                                       Página de error
css/estilos.css                                Todo el CSS
js/app.js                                      Horario abierto/cerrado, cookies, eventos dataLayer, mapa, formulario
fonts/                                         Saira (woff2), copia incrustada para doble clic y licencia OFL
img/                                           Las 3 fotos de obra de la web actual (WebP + JPG)
robots.txt  sitemap.xml  llms.txt
docs/jsonld/                                   Copia del JSON-LD para revisarlo
```

## Arquitectura SEO prevista

Ya están enlazadas (con `data-pendiente`; en el prototipo muestran un aviso) y comentadas en `sitemap.xml`:
- **Servicios:** `/alta-tension/`, `/baja-tension/`, `/termografias/`, `/eficiencia-energetica/`, `/automatizacion-industrial/` y `/telecomunicaciones/`.
- **Provincias:** `/instalaciones-electricas-gipuzkoa/` y `/instalaciones-electricas-alava/`.

Para crear cada una, copia `mantenimiento-centros-transformacion/index.html` y cambia los textos, el `title`, la `description`, el `canonical` y el JSON-LD. Después quita `data-pendiente` de sus enlaces y descomenta su URL en `sitemap.xml`.

## Datos a confirmar con el cliente

1. Categoría y nº de registro como empresa autorizada en **alta tensión**. Su web dice «nivel C, RD 223/08».
2. Si la certificación **ISO 9001 / ISO 14001** sigue vigente. Su web cita las versiones de 2000 y 2004, que ya no existen.
3. Que las **fotos** son de obras propias; ubicación y año de cada obra, y fotos en alta resolución (las actuales son de 630 px).
4. El alcance exacto del **contrato de mantenimiento de CT**: si incluye termografía, potencias de los transformadores de reserva y tiempos.
5. El **resumen normativo** de la landing (RD 337/2014, inspección OCA cada 3 años en AT y cada 5 en BT).
6. **Coordenadas exactas**, NIF y ficha de Google Business Profile.
7. El logotipo en **vector original**.
8. **Traducción** al euskera.

## Antes de publicar

- **Formulario:** conectar el `action` a un servicio de envío (ver `js/app.js`).
- **Analítica:** descomentar el snippet de GTM/GA4 en `cargarAnalitica()`. Solo se carga tras aceptar las cookies.
- **Textos legales:** que los revise una asesoría.
- **Euskera:** si `/eu/` se publica sin traducir, añadir `noindex` en `eu/index.html` y quitar las líneas `hreflang="eu-ES"`.
