# Arqueo de Caja

App HTML standalone para registro y arqueo de efectivo en congregación.

## Estructura

- Archivo único: index.html
- Sin dependencias locales (librerías vía CDN)
- Librerías: jsPDF, html2canvas, SignaturePad 4.1.7, IBM Plex fonts

## Secciones

1. **Sobres** — consecutivo + valor (COP). Cada sobre tiene un checkbox "Consig." para marcarlo como soporte de consignación bancaria: estos sobres se reportan pero no traen efectivo, por lo que se excluyen del total de sobres y del cuadre. En pantalla se muestran atenuados/tachados; en la vista de impresión aparecen en azul claro con etiqueta CONSIG. y valor tachado.
2. **Billetes y monedas** — denominaciones COP ($100K–$1K billetes, $1K–$50 monedas)
3. **Consignación** — billetes + monedas - retiro para caja
4. **Personas** — roles: Anciano, Tesorero, Diácono, Quien consigna
5. **Firmas digitales** por persona (SignaturePad)

## Cuadre

Banner en tiempo real: Total Sobres (excluye consignación) vs Total Efectivo → Diferencia y estado (exacto / sobra / falta).

## Salidas

- Vista de impresión (preview HTML)
- Imprimir carta (window.print con @page letter)
- Descargar PDF (jsPDF + html2canvas, tamaño carta, márgenes 2cm)

## SignaturePad — notas móvil

El modal de firma usa `setTimeout(60ms)` en lugar de `requestAnimationFrame` para garantizar que el elemento `position: fixed` esté pintado antes de medir el canvas. El tamaño se lee con `getBoundingClientRect()`. La firma existente se dibuja en espacio CSS (no físico) porque SignaturePad ya escala el contexto por `devicePixelRatio` en su constructor.
