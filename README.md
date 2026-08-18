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

### Constante o editable

Un botón con forma de **candado** decide cómo se comporta el flujo, y al pasar el mouse por
encima explica la diferencia:

- **Flujo constante** (como arranca el sitio): las casillas quedan fijas y los cinco años son
  iguales, tal como el ejercicio original. Sólo se cambia la cantidad de portones.
- **Flujo editable**: cada casilla de cada año se puede modificar, para simular inflación, un
  año malo o dejar de pagar arriendo.

Elegir un escenario que necesita años distintos desbloquea el flujo automáticamente, y
*Restaurar caso base* devuelve todo —cifras, tasa y candado— a su estado inicial.

### Las casillas

Dentro de **Evaluación → Caso Práctico**, las 47 casillas de los dos flujos de caja son
editables, año por año. Ningún año tiene por qué parecerse al anterior: se puede subir la
producción del año 3, aplicar inflación a los costos, dejar el arriendo en cero o cambiar la
inversión inicial. Cada vez que se toca una casilla se recalcula todo desde cero.

La fila *Ingresos por Ventas* trae además un contador de unidades (1 a 60) con botones − y +,
que aplica la misma producción a los cinco años de una vez. Las filas de operación son las
mismas en ambas tablas —es el mismo taller, lo único que cambia es cómo se financia—, así que
editarlas en cualquiera de las dos actualiza las dos.

El botón con forma de **ojo** abre una ventana emergente que oscurece el fondo y entrega el
análisis completo del escenario que esté en pantalla en ese momento:

- **PRI** de cada caso, calculado acumulando los flujos año a año (no dividiendo la inversión
  por el flujo, porque con años distintos ese atajo no sirve)
- **VAN** y **TIR** (obtenida por bisección), con el veredicto correspondiente. La
  **rentabilidad exigida es editable** de 0% a 100%: al subirla, el mismo proyecto vale menos, y
  al llegar a la TIR el VAN cae a cero y el veredicto avisa que ahí deja de convenir. Como cada
  caso tiene su propia TIR, se ve que exigiendo un 60% el flujo puro se rechaza mientras el
  financiado todavía crea valor
- El recorrido año por año del flujo acumulado, marcando en verde el año en que cada caso
  recupera su inversión
- Cinco escenarios listos para mostrar en clase: caso base, producción creciente, inflación del
  5% en los costos, taller sin arriendo y un año malo

El modelo de partida:

| Concepto | Valor | ¿Depende de cuánto produzcas? |
|---|---|---|
| Inversión inicial (Caso A) | $4.500.000 | — |
| Capital propio + crédito (Caso B) | $2.000.000 + $2.500.000 | — |
| Precio de venta de un portón | $1.000.000 | Sí, por unidad |
| Fierros e insumos por portón | $500.000 | Sí, por unidad |
| Arriendo y luz del taller | $2.400.000 al año | **No** |
| Administración y marketing | $1.200.000 al año | **No** |
| Cuota del préstamo (Caso B) | $800.000 al año | **No** |

Ahí está la lección principal: como los costos fijos no se mueven, **la ganancia crece mucho más
rápido que las ventas**. Al pasar de 12 a 24 portones al año las ventas se duplican, pero el
flujo neto se multiplica por cuatro. Las filas que no dependen de la producción están marcadas
con la etiqueta *«costo fijo»*, y el escenario de inflación deja ver el efecto contrario: con
los mismos ingresos, el margen se estrangula de $2.400.000 a $331.139 en cinco años.

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
