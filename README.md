# Propuesta Qiu Commerce — Escuela de Golf en Lechería

Landing page de una sola página con el catálogo de equipamiento de driving range, la investigación de demanda, precios por volumen y una calculadora de pedido que arma el mensaje de WhatsApp automáticamente.

**Archivo a publicar:** `index.html` (autocontenido — no necesita servidor, base de datos ni build)

---

## 1. Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub.
2. Sube `index.html` a la raíz. Por interfaz web arrastra el archivo, o por consola:

   ```bash
   git init
   git add index.html README.md
   git commit -m "Propuesta Escuela de Golf en Lechería"
   git branch -M main
   git remote add origin https://github.com/TU-USUARIO/TU-REPO.git
   git push -u origin main
   ```

3. En el repositorio: **Settings → Pages**.
4. En *Source*, elige la rama `main` y la carpeta `/ (root)`. Guarda.
5. En 1–2 minutos tendrás el link público:

   ```
   https://TU-USUARIO.github.io/TU-REPO/
   ```

6. Ese es el link que se comparte con la academia por WhatsApp, correo o Instagram.

> **Dominio propio (opcional):** si quieres publicarlo como `golf.qiuagency.com`, crea un archivo `CNAME` en la raíz del repo con esa dirección dentro, y apunta un registro CNAME en tu DNS hacia `TU-USUARIO.github.io`.

---

## 2. El recorrido de la página

La página está construida como un recorrido guiado de seis estaciones, señalizadas con marcadores de yardas como en un campo de práctica. En pantallas grandes aparece un riel de progreso a la izquierda que se va iluminando.

| Estación | Sección | Qué hace |
|---|---|---|
| — | Portada | Plantea la propuesta y lanza la estela de la bola |
| 50 m | La demanda | Cuatro datos del sector que sustentan la inversión |
| 100 m | El vacío | El problema de la academia frente a lo que ofrece Qiu |
| 150 m | El catálogo | 11 productos con precio sugerido y costo estimado |
| 200 m | Tu pedido | Calculadora con descuento por volumen automático |
| 250 m | Fases | Plan de implementación en tres etapas |
| 300 m | Cerrar | Datos de contacto y llamado final |

---

## 3. La calculadora de pedido

Es la pieza que convierte. La academia ajusta cantidades y la página:

- aplica sola el descuento por volumen que corresponde a cada categoría,
- muestra subtotal, ahorro y total,
- y compone el mensaje de WhatsApp **con el pedido ya escrito**, línea por línea.

Cuando el cliente presiona *Enviar pedido por WhatsApp*, a Qiu le llega un mensaje del tipo:

```
Hola Qiu Commerce, soy de la Escuela de Golf MA en Lechería.
Quiero cotizar este pedido:

• 20 × Cesta plástica driving range — US$288.00 (-10%)
• 2 × Dispensador manual sin electricidad — US$266.80 (-8%)

Subtotal: US$610.00
Ahorro por volumen: US$55.20
Total estimado: US$554.80

¿Me confirman disponibilidad y tiempo de entrega?
```

---

## 4. Cómo poner FOTOS REALES de los productos

Hoy cada producto usa un render vectorial hecho a medida. Para sustituirlo por foto real:

1. Guarda la imagen en la carpeta `fotos/` (por ejemplo `fotos/cesta-metalica.jpg`).
   Recomendado: 800×600 px o mayor, formato JPG o WebP, bajo 300 KB.
2. Abre `build.py`, busca el producto y cambia `foto=None` por la ruta:

   ```python
   dict(id="ces-met", sku="QC-CB-02", nom="Cesta metálica de alambre",
        ...
        foto="fotos/cesta-metalica.jpg"),
   ```

3. Vuelve a generar la página:

   ```bash
   python3 build.py
   ```

4. Sube el `index.html` actualizado **y** la carpeta `fotos/` al repositorio.

Se pueden mezclar: los productos con `foto` definida muestran la imagen, el resto conserva el render vectorial.

### De dónde sacar las fotos legalmente

Las imágenes de los listados de Alibaba, Amazon o eBay pertenecen a esos vendedores; copiarlas a un catálogo comercial propio expone a un reclamo de derechos de autor. Las tres vías correctas:

1. **Pedírselas al proveedor.** Es práctica estándar en Alibaba: al negociar el pedido se solicita el *product image pack* para revendedores. La mayoría lo entrega sin costo y con permiso de uso comercial.
2. **Fotografiar la mercancía** al llegar el primer embarque. Es lo que más conviene a mediano plazo: fotos propias, con la marca Qiu, sin depender de nadie.
3. **Bancos de imágenes con licencia comercial** para fotos genéricas de ambiente (campo de práctica, pelotas), no para producto específico.

---

## 5. Cambiar el número de WhatsApp o los precios

- **Número de WhatsApp:** está en `build.py` en la constante `TEL` (formato internacional sin `+`, por ejemplo `584248831167`). Cambia ahí y regenera. Si prefieres editar el HTML directamente, busca y reemplaza `584248831167` (aparece 6 veces).
- **Precios, descuentos, textos de producto:** todo vive en la lista `P` dentro de `build.py`. Los tramos de descuento se definen como `tramos=[[10,.10],[30,.18]]`, que se lee: desde 10 unidades 10%, desde 30 unidades 18%.
- Tras cualquier cambio: `python3 build.py` y vuelve a subir `index.html`.

---

## 6. Archivos del repositorio

```
index.html      la página lista para publicar (autocontenida)
build.py        generador: datos de producto, precios y renders
template.html   plantilla base con estilos y estructura
fotos/          carpeta para las fotos reales de producto
README.md       este archivo
```

Para publicar basta con `index.html`. El resto se incluye para poder actualizar el catálogo después.

---

## 7. Detalles técnicos

- Sin dependencias ni framework. Un archivo, abre en cualquier navegador.
- El catálogo es HTML estático: se ve completo aunque el JavaScript falle. El JS solo activa la calculadora y el riel de progreso.
- El logo va incrustado en base64: no hay que subir archivo de imagen aparte.
- Responsivo verificado de 360 px a 1920 px.
- Contraste de texto conforme a WCAG AA en todas las secciones.
- Respeta `prefers-reduced-motion` para quien tenga desactivadas las animaciones.
- Tipografías desde Google Fonts con alternativas del sistema si no cargan.

---

Qiu Commerce × Qiu Agency · qiuagency2023@gmail.com · +58 424-8831167
