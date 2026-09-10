# NEXUS-X

Nueva arquitectura limpia para gestión e investigación de laboratorio escolar.

## Regla de identidad
**1 registro = 1 ID NEXUS-X.** Las columnas/campos restantes son atributos del mismo registro. No se generan códigos por columna.

## Fuente maestra
El Word `data/Sustancias_Lab_BASE_NEXUS-X.docx` es la fuente humana. Para rendimiento, el navegador arranca desde `data/inventory.json`, generado y validado a partir del Word. El botón **Cargar Word maestro** vuelve a parsear el DOCX y solo reemplaza la base si la validación completa pasa.

## Funciones
- Dashboard con estética inspirada en la interfaz proporcionada.
- Inventario local-first con búsqueda y filtros.
- Excel manual para importación y CSV para exportación.
- Investigación local con evidencia y búsqueda web opcional.
- IA opcional mediante endpoint compatible con OpenAI; nunca es requisito para el inventario.
- QR con cámara; al detectar, la cámara se detiene y se oculta antes del resultado.
- Carga de PDF bajo demanda.
- PWA y caché del núcleo.
- Diagnóstico de integridad.

## Validación
Con Node.js:

```bash
node tools/validate.mjs
```

La validación comprueba archivos esenciales, 111 registros, IDs únicos, formato `NEXUS-X-0001`…`NEXUS-X-0111`, sintaxis JS e IDs HTML duplicados.

## Nota sobre librerías pesadas
SheetJS, JSZip y PDF.js se cargan **solo al utilizar Excel, Word o PDF**. Esto reduce el trabajo de arranque en equipos escolares de pocos recursos. Si no hay Internet y la librería aún no está en caché, la función correspondiente mostrará un error sin romper el resto de NEXUS-X.
