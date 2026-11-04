Informe de progreso del rediseño

Todo lo que sigue sale de lo que he hecho en esta conversación y de una comprobación de solo lectura que acabo de ejecutar. No he modificado nada para escribir este informe.

1. Resumen general

Objetivo. Mejorar la capa visual y de uso de la web existente conservando funcionalidades y datos. “La web” es una sola página: el demo.html que genera build_demo.py a partir de los JSON de las tiendas. No hay framework, rutas, autenticación ni API; el resto del proyecto (lectores, emparejador, base de datos) no forma parte del rediseño.

Estrategia.

Auditar el estado actual con capturas reales.
Seguir el proceso de Taste para pantallas de aplicación. Su herramienta draw.mjs repartió el estilo “Data terminal”: lista única en vez de tarjetas, cifras tabulares, una sola línea de acento de 1 px para toda selección y poco color.
Cumplir el “suelo de calidad” de Impeccable.
Reescribir la plantilla de la página manteniendo el contrato de datos y los comandos.

Punto exacto. La versión 1 del rediseño está escrita y generada, pero no verificada visualmente. El último paso fue abrirla en el navegador y mirarla, y lo detuviste antes de que yo la viera.

Progreso: aproximadamente un 35–40 %.

Fase	Peso	Estado	Computo
Auditoría	10 %	Hecha	10
Dirección artística	10 %	Hecha	10
Implementación v1	35 %	Escrita, sin verificar	~18
Verificación, iteración y pasadas de crítica	25 %	Casi sin empezar	~2
Entrega (README, claudecode.md, ZIP, informe)	20 %	Sin empezar	0

El código escrito sin ver el resultado cuenta solo a medias, porque es la parte que más cambia al mirarla.

2. Modificaciones realizadas

Todas están en build_demo.py. Están escritas y generan la página, pero ninguna está verificada visualmente.

Página rediseñada: la página única de comparación.

Componentes nuevos o reescritos

Cabecera con título y línea de metadatos (nº de tiendas, productos, fecha de los datos).
Aviso de página de ejemplo.
Buscador con icono dibujado.
Selectores de idioma, tipo y orden, con la línea de acento de 1 px.
Dos interruptores: “Solo con stock” y “Parejas sin confirmar”.
Contador de resultados como región accesible.
Panel único con una cabecera de columnas.
Un grupo por producto con su <table> semántica.
Etiqueta “Mejor compra” subrayada con la línea de acento.
Estado con punto más texto (no solo color).
Enlace con icono SVG dibujado.
Separador “Parejas sin confirmar”.
Estados vacío (dos variantes) y de error.
Botón “Mostrar N más”.
Pie con las fuentes de datos.
Enlace “Saltar a la lista”.

Mejoras visuales

Fuentes Public Sans e IBM Plex Mono, incrustadas en el HTML.
Tokens de color para tema claro y oscuro.
Precios alineados a la derecha en tipografía monoespaciada.
Mejor compra marcada con peso y línea, no con un relleno verde.
Nombres de producto sin el idioma repetido (“- Ingles”, “[ES]”).

Responsive. Un punto de corte a 640 px, objetivos táctiles de 44 px con pointer: coarse, pestañas con desplazamiento horizontal, campo de 16 px para evitar el zoom de iOS y columnas más estrechas. Está escrito, no probado.

Mejoras de uso

Orden por mejor compra, precio o nombre.
Paginación visible en lugar del tope silencioso de 80.
Filtros guardados en la dirección (#q=…).
Movimiento limitado a la línea de acento, con respeto a prefers-reduced-motion.
Selección de texto, cursor, barras de desplazamiento y subrayado con el tema.

Cambios técnicos. Sin peticiones a internet; archivo de unos 163 KB. Contrato de datos y firmas de funciones intactos, y los comandos de generación son los mismos.

3. Archivos
Archivo	Acción	Detalle
build_demo.py	Modificado	191 → 455 líneas. Plantilla HTML/CSS/JS nueva y funciones nuevas clean_name y font_css.
assets/fonts/	Creado	7 fuentes .woff2 y 2 licencias OFL.
Resto del proyecto	Sin tocar	tests/, tcg_compare/, run.py, match.py, README.md, samples/.

Fuera del proyecto, temporales: /home/claude/demo_nuevo.html, draw_sheet.txt, shots/*.png y la carpeta pw/ (Chromium y Playwright para npm).

Entregado a ti, sin cambios: tcg-compare.zip y demo_ejemplo.html en outputs, ambos del 27/10 y con el diseño antiguo.

4. Tareas pendientes, por prioridad

Prioridad 1: verificar y corregir la v1

Mirar las 3 capturas v1 (existen en disco, las generé a las 09:23, pero no las he visto) y corregir lo que falle.
Probar a 320, 390, 768 y 1280 px, en claro y oscuro: desbordamientos, solapes, “Mejor compra” partiéndose, pestañas.
Probar las interacciones con el navegador: búsqueda, pestañas, interruptores, estado vacío, “Mostrar más” y la dirección con filtros.
Comprobar teclado y foco.
Probar con el volumen real (223 productos y 236 dudosas), no con 5 de ejemplo.
Calcular el contraste con números. Las razones que tengo son estimaciones mías, no mediciones.

Defectos que sospecho sin haberlos comprobado

Posible doble línea entre la cabecera de columnas y el primer grupo: la regla .panel>.grp:first-of-type probablemente no aplica, porque los grupos están dentro de #list.
Usé la clase .num (monoespaciada) en frases enteras: línea de metadatos, contador y pie. Eso es monoespaciada como disfraz; solo debe ir en las cifras.
En móvil subo el tamaño base un 6,25 %, y el estilo de Taste fija 13 px; no sé cómo se ve.
En oscuro, los separadores (
#1b1a1f) pueden ser casi invisibles.
El tema claro lo derivé yo; Taste solo dibujó el oscuro.

Prioridad 2: pasadas de calidad
7. Ejecutar lint e inspect de Taste, y el detector de Impeccable (no he ejecutado ninguno).
8. Leer los playbooks de Impeccable (critique, audit, polish), que no he leído.
9. Completar la lectura de app-screens.md, que no he leído entero.
10. Segunda pasada de crítica visual.

Prioridad 3: entrega
11. Regenerar samples/demo_ejemplo.html con el diseño nuevo.
12. Tests nuevos: sin peticiones externas, estructura, contraste.
13. Actualizar el README.
14. claudecode.md: tu petición anterior sigue sin hacer, y no sé si la quieres tras el prompt de rediseño.
15. ZIP nuevo, verificado (descomprimir, ejecutar tests, generar la demo).
16. Informe final.

Prioridad 4: refinamiento opcional. Revisión de textos y hueco de diseño para los gastos de envío cuando tengamos datos.

5. Skills y herramientas
Herramienta	Uso real	Aportación
Taste (design-taste-frontend)	Parcial. Leí el SKILL.md en gran parte y de app-screens.md solo las secciones del proceso, tablas y listas, estados y móvil. Ejecuté draw.mjs dos veces (mismo resultado).	Estilo, tokens, tipografía y la regla de la línea de acento.
Impeccable	Parcial. Leí SKILL.md y craft-floor.md.	El suelo de calidad y la lista de lo que hay que evitar.
Resto de skills (animate, emil-design-eng, mobile-native…)	No usadas.	—
Playwright	Parcial. Usé playwright-core con un Chromium empaquetado en npm. No es el conector de Playwright de Claude.ai.	4 capturas del diseño antiguo (vi 2) y 3 del nuevo (no las vi).
Figma MCP	No usado ni comprobado. No me diste archivos de Figma, así que no tenía qué consultar.	—

Impeccable no cargó su contexto. Su comando context falló por permisos y, al repetirlo con sh, mi carpeta de trabajo ya no existía y devolvió un contexto vacío.

Incidencia a conocer: el entorno se reinició a mitad de la tarea. Tuve que restaurar el proyecto desde el ZIP de outputs.

6. Verificación y calidad
Ejecutado: los 145 tests de Python pasan (3 se saltan sin base de datos). La página nueva se genera sin errores.
Diseño antiguo: lo rendericé en Chromium a 1280 px (claro y oscuro) y 390 px, sin errores de consola. Vi dos de esas capturas.
Diseño nuevo: hay 3 capturas en disco que no he visto. No tengo ningún resultado de consola ni de aspecto. No puedo afirmar que se vea bien ni que no tenga errores.
No hecho: pruebas responsive del diseño nuevo, interacciones, teclado, contraste medido, node --check del JavaScript nuevo y el linter de ninguna skill.
Errores detectados: solo en el diseño antiguo (listados en la auditoría). En el nuevo solo tengo las sospechas de arriba.
7. Estado y recuperación
¿Guardado? Está escrito en disco en /home/claude/tcg-compare. No está en ningún ZIP entregado: el que tienes en outputs es el anterior al rediseño.
Sin guardar: no hay nada pendiente de guardar, porque cada edición se escribe al instante. Los temporales son los de la sección 3.
Riesgo real: esa carpeta es volátil, ya se perdió una vez. Si se reinicia otra vez, perdería la v1; las fuentes se pueden volver a descargar.
¿Puedo recuperar todo? Sí mientras no haya reinicio. El diseño antiguo sigue intacto en el ZIP de outputs.
¿Puedo generar un ZIP del estado actual? Sí, pero no lo he hecho porque pediste no modificar nada. Crearía un archivo nuevo (con otro nombre) y no tocaría el ZIP anterior.
¿Continuar sobrescribe algo? Las ediciones son sobre build_demo.py, y el original se conserva en el ZIP antiguo. No sobrescribiría ningún archivo de outputs sin avisarte.
8. Trabajo restante

Cuatro bloques de trabajo: verificar y corregir (prioridad 1), pasadas de calidad con las herramientas (prioridad 2), tests, documentación y claudecode.md (prioridad 3), y ZIP con su verificación. Calculo unas 10 a 14 iteraciones de trabajo, y la mayor parte está en el primer bloque, porque lo que salga al mirar la v1 decide el resto.

Primera tarea concreta: guardar un ZIP de seguridad y ver las 3 capturas.

9. Recomendación

Dividir el trabajo en tres fases, empezando por un ZIP de seguridad.

Fase A: guardar el estado actual como ZIP aparte, y verificar y corregir la v1 con el navegador real.
Fase B: pasadas de calidad: lint e inspect de Taste, el detector de Impeccable y contraste medido.
Fase C: documentación, claudecode.md, ZIP final verificado e informe.

Lo justifico así. Un reinicio ya me costó una carpeta de trabajo, y todavía no he visto la v1. Si sigo escribiendo sin mirar, puedo acumular errores sobre algo que se ve mal.

Necesito que me digas:

¿Autorizas el ZIP de seguridad?
¿Sigues queriendo claudecode.md?
¿Te vale el tema claro derivado por mí? Es un criterio mío, no de Taste.

Opcional: si me adjuntas tu demo.html real, la probaré con tus 223 productos.

No toco nada hasta que me autorices.
