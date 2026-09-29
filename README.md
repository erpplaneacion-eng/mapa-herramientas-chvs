# Mapa de herramientas CHVS

Página interactiva con las herramientas digitales que construyó el **Área de Mejoramiento · Transformación Digital** de la Corporación Hacia un Valle Solidario.

**Enlace público:** https://erpplaneacion-eng.github.io/mapa-herramientas-chvs/

Se abre con un clic, sin registrarse. Está publicada con GitHub Pages desde la rama `main` de este repositorio.

## Qué muestra

- **Tablero de proyectos:** una tarjeta por herramienta, con filtros por área y un buscador. Al tocar una tarjeta se abre su ficha, que dice qué hace, cómo funciona paso a paso, qué gana la Corporación, con qué se construyó y dónde está alojada.
- **Tres estados:**
  | Estado | Cómo se ve | Cuándo se usa |
  | --- | --- | --- |
  | En línea | Marca verde y botón «Abrir herramienta» | Tiene enlace público |
  | En construcción | Borde dorado y barra de avance | Todo lo que no está terminado |
  | Uso interno | Marca gris | Proceso automático o línea privada, sin enlace público |
- **Alianzas:** son proyectos hechos con otras entidades; la tarjeta muestra el nombre del aliado.
- **Dónde viven y tecnologías:** conteo por plataforma (Railway, Firebase, Apps Script, AppSheet, RunPod, equipo local) y el stack utilizado.

Identidad visual según el manual de marca CHVS 2026: fondo blanco, degradados verdes (`#76B82A` → `#00923E`), títulos en League Spartan, textos en Poppins y el logo de Mejoramiento.

## Estructura

```
mapa-herramientas-chvs/
├── index.html        ← la página publicada (se genera, no se edita a mano)
├── README.md
└── fuente/           ← archivos de trabajo, solo en el equipo local (no se suben)
    ├── datos.js      ← LA LISTA DE HERRAMIENTAS: aquí se hacen casi todos los cambios
    ├── plantilla.html← estructura y lógica de la página
    ├── estilo.css    ← colores, tipografía y diseño
    ├── armar.js      ← une plantilla + estilo + datos + logos en un solo HTML
    └── publicar.sh   ← regenera index.html y lo sube a GitHub
```

El isotipo se toma de `../isotipo_chvs.png` y va incrustado dentro de la página. El logo de Mejoramiento va como vector dentro de `armar.js`.

## Cómo actualizar

1. Editar `fuente/datos.js`. Cada herramienta es un bloque así:

   ```js
   {a:"gh",                       // área: gh, bien, comp, cal, com, ext
    n:"Nombre de la herramienta",
    l:"https://…",                // enlace público (opcional)
    q:"Qué hace, en una frase.",
    p:["Paso 1","Paso 2","Paso 3"],
    b:"Beneficio para la Corporación.",
    t:["Django","PostgreSQL"],    // tecnologías
    h:["Railway"],                // dónde se aloja
    e:{tipo:"construccion",pct:40,nota:"En construcción."}, // opcional
    interno:true,                 // opcional: uso interno, sin enlace
    al:"En alianza con …"}        // opcional: solo para el área ext (Alianzas)
   ```

   Las áreas son estas: `gh` Gestión Humana · `bien` Bienestar y SST · `comp` Compras y Contabilidad · `cal` Calidad y Logística · `com` Comunicaciones · `ext` Alianzas.

2. Publicar desde la carpeta `mapa-herramientas-chvs`:

   ```bash
   bash fuente/publicar.sh "Describe el cambio"
   ```

   El script arma la página, revisa que el código no tenga errores, genera `index.html`, hace el commit y lo sube. GitHub Pages lo muestra en uno o dos minutos, en el mismo enlace.

Requisitos: Node.js y Git con acceso a la cuenta `erpplaneacion-eng`.

## Reglas acordadas

- El ERP no va en este mapa.
- En CAVASA no se menciona el envío por WhatsApp, porque no está operativo.
- Todo lo inacabado se marca «En construcción», con su porcentaje cuando se conoce.
- Si una herramienta no tiene enlace público, va como «Uso interno».
- Los enlaces de `vallesolidario.com` (Apps Script) solo abren con una cuenta de la Corporación.
