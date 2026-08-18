# Evaluación y Gestión de Proyectos — LIR 2026

Sitio web de la **Semana TP** del Liceo Industrial de Rengo. Reúne en un solo archivo los dos
módulos de la unidad: cómo saber si un proyecto técnico es rentable, y cómo llevarlo a cabo
sin perder el control de los plazos.

## El sitio

Todo vive en **[`proyecto-tp.html`](proyecto-tp.html)**: un único archivo, sin dependencias
locales ni proceso de compilación. Se abre haciendo doble clic.

Existe además **[`proyecto-tp-offline.html`](proyecto-tp-offline.html)**, idéntico en contenido
pero con Tailwind, Three.js, Font Awesome, las tipografías y los logos incrustados dentro del
propio archivo. Pesa unos 2,4 MB y **funciona sin conexión a internet**: es el que conviene
llevar al stand por si la red falla. El archivo normal es más liviano y es el que se publica en
la web.

Contiene dos módulos que se navegan entre sí:

| Módulo | Contenido | Ruta |
|---|---|---|
| **Evaluación de Proyectos** | Generación de la idea, estudios de formulación, flujo de caja puro y financiado, VAN, TIR, PRI, marketing, y un caso práctico a 5 años de un taller de portones | `#/evaluacion` |
| **Gestión de Proyectos** | Acta de constitución, alcance, Carta Gantt, control de cambios, liderazgo y cierre | `#/gestion` |

Se salta de uno al otro con el botón de la barra superior o con la tarjeta al pie de cada módulo.

### Enlaces directos

Cada etapa tiene su propia dirección, y funciona aunque se entre desde el otro módulo:

```
proyecto-tp.html#/gestion     abre el módulo de Gestión
proyecto-tp.html#ev-e4        abre Evaluación en la Etapa 4 (VAN)
proyecto-tp.html#ge-caso      abre Gestión en el caso práctico
```

## El simulador del caso práctico

Dentro de **Evaluación → Caso Práctico**, la fila *Ingresos por Ventas* de cada tabla trae un
campo con la cantidad de unidades al año (de 1 a 60), con botones − y +. Las dos tablas comparten
el mismo número: al cambiarlo en cualquiera de ellas, ambas se recalculan enteras —ingresos,
costos de insumos, flujo neto, periodo de recuperación y los textos de conclusión.

El botón con forma de **ojo** abre una ventana emergente que oscurece el fondo y explica el
escenario: el ritmo de trabajo, las ventas del año, el flujo neto de los dos casos, el punto de
equilibrio y de dónde sale cada número. Se cierra con el mismo ojo, con la tecla Escape o
pulsando fuera de ella.

El modelo que hay detrás es el mismo del ejercicio original:

| Concepto | Valor | ¿Cambia al producir más? |
|---|---|---|
| Precio de venta de un portón | $1.000.000 | Sí, por unidad |
| Fierros e insumos por portón | $500.000 | Sí, por unidad |
| Arriendo y luz del taller | $2.500.000 al año | **No** |
| Administración y marketing | $1.500.000 al año | **No** |
| Cuota del préstamo (Caso B) | $800.000 al año | **No** |

Ahí está la lección: como los costos fijos no se mueven, **la ganancia crece mucho más rápido
que las ventas**. Al pasar de 12 a 24 portones al año las ventas se duplican, pero el flujo neto
se multiplica por cuatro ($2.000.000 → $8.000.000). Las filas que no cambian están marcadas en
la tabla con una etiqueta *«no cambia»*, y el simulador avisa cuando la producción cae bajo el
punto de equilibrio (8 portones al año), donde el taller deja de ganar dinero.

## Cómo está hecho

- **Tailwind CSS** (vía CDN) para los estilos, con una paleta *neon* propia
- **Three.js** para el fondo 3D animado
- **Font Awesome** e **Inter / Orbitron** para iconografía y tipografía

Como todo se carga desde CDN, hace falta conexión a internet la primera vez.

### El fondo animado

La grilla avanza en un bucle infinito sin cortes visibles. El truco: el relieve se genera en un
bloque de 8 filas que se repite a lo largo del plano, de modo que al desplazarse exactamente 40
unidades cada vértice queda sobre otro de idéntica altura y el ciclo reinicia sin que se note.
El borde lejano del plano queda disuelto en la niebla, y el movimiento se calcula por tiempo
real —no por fotograma—, así la velocidad es la misma en pantallas de 60 Hz y de 144 Hz.

## Ver el sitio localmente

Basta con abrir el archivo. Si prefieres servirlo por HTTP:

```bash
python -m http.server 8765
```

Luego visita `http://localhost:8765/proyecto-tp.html`.

## Créditos

Sitio desarrollado por **Diego Román Muñoz**, Ingeniero en Informática.
Semana TP — Liceo Industrial de Rengo (LIR 2026), Chile.
