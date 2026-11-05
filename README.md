# Plantillas LaTeX del Consejo de Estudiantes de Ciencias

Plantillas de los documentos del Consejo de Estudiantes (antes Delegación de
Estudiantes) de la Facultad de Ciencias de la Universidad de Zaragoza, pensadas
sobre todo para quien lleva la Secretaría. Todos los ejemplos usan nombres y
fechas inventados.

## Qué hay

| Carpeta | Archivo | Para qué |
|---|---|---|
| `actas/` | `acta.tex` | Acta de un pleno, con la asistencia en una columna estrecha a la izquierda |
| `actas/` | `convocatoria.tex` | Convocatoria de pleno con su orden del día |
| `actas/` | `resolucion.tex` | Resolución de la Secretaría (p. ej., representantes en comisiones) |
| `actas/` | `certificado.tex` | Informe favorable de pertenencia y participación, para pedir créditos por el [Acuerdo 2020.23 de la Junta de Facultad](https://ciencias.unizar.es/sites/ciencias/files/users/fmlou/pdf/acuerdosjuntafacultad/2020_23_criterios_reconoc_creditos_activ_repres_report.pdf) |
| `documentos/` | `documento.tex` | Documento largo (informes, propuestas, comparativas), con secciones y pie de página |

Las cuatro plantillas de `actas/` comparten `acta-consejo.sty` (maquetación,
marca «BORRADOR», bloque de firma) y `config.tex`. La de `documentos/` usa
`estilo-consejo.tex`. Las dos familias tienen la misma página.

## Identidad corporativa

La página sigue las medidas del «oficio» del
[Manual de identidad corporativa de la Universidad de Zaragoza](https://gic.unizar.es/sites/gic/files/identidadCorporativa/manual-completo-1474.pdf)
(págs. 60 y 82), adaptadas al Consejo:

- **Logotipo del Consejo** (`logo_consejo.pdf`) arriba a la izquierda: 60 mm de
  ancho, a 25 mm del borde superior y 10 mm del izquierdo.
- **Sello de la Facultad de Ciencias en fondo de agua** (`sello_ciencias_agua.pdf`)
  en el margen inferior derecho: recortado a los 2/3 superiores izquierdos,
  como indica el Manual, tramado al 10 % del Pantone 653, en una caja de
  155 mm de ancho cuyo borde superior queda a 150 mm del inferior.
- **Dirección** en el margen inferior izquierdo, a 15 mm de los bordes.
- **Tipografía:** Myriad Pro, la del Manual, si tienes sus archivos (ver
  [Usar Myriad Pro](#usar-myriad-pro)). Si no, Source Sans (paquete
  `sourcesans`), su pariente libre. Si tampoco está, Helvetica, y se avisa
  en el log.
- **Color:** azul Pantone 653 (`#223D71`, color `azulUZ`) para títulos y
  cabeceras de tabla.
- No se incluye el complemento «unizar.es», porque los documentos son del
  Consejo y no de la Universidad.

El logotipo es el que fija el Anexo del Reglamento del Consejo de Estudiantes.
Para cambiarlo, sustituye `logo_consejo.pdf` en las dos carpetas.

## Al empezar un curso

Solo hay que tocar `actas/config.tex`:

- `\firmante` y `\cargofirmante`: quien firma.
- `\setorgano{el}{Consejo de Estudiantes}`: el nombre del órgano. Los textos
  lo usan con `\organo`, `\elorgano` y `\delorgano`, así que si vuelve a
  cambiar basta con tocar esta línea (con `la` o `el` según el artículo).
- `\borradortrue` o `\borradorfalse`: la marca «BORRADOR» de fondo. Quítala
  solo en la versión que se firma.

La dirección del pie se cambia redefiniendo `\direccionacta` (en `actas/`) o
`\direcciondoc` (en `documentos/`).

## Compilar

Con LuaLaTeX (la primera línea de cada `.tex` lo indica). También compilan
con XeLaTeX y con pdfLaTeX, pero con pdfLaTeX nunca se usa Myriad Pro. En
local:

```bash
latexmk acta.tex
```

En Overleaf: descarga el `.zip` de la carpeta que necesites desde
[Releases](../../releases) (o «Code → Download ZIP»), y en Overleaf
«New Project → Upload Project». Después, en «Menu → Compiler», elige
**LuaLaTeX** (Overleaf no lee la primera línea del `.tex`).

## Usar Myriad Pro

Myriad Pro es de pago, así que sus archivos no están en el repositorio (el
`.gitignore` impide subirlos). Las plantillas la usan solas si la encuentran:

1. Consigue estos cuatro archivos de Myriad Pro (por ejemplo, los de una
   instalación de Adobe):

   | Archivo | Estilo |
   |---|---|
   | `MyriadPro-Regular.otf` | Redonda |
   | `MyriadPro-Bold.otf` | Negrita |
   | `MyriadPro-It.otf` | Cursiva |
   | `MyriadPro-BoldIt.otf` | Negrita cursiva |

   Tienen que llamarse exactamente así. Si los tuyos tienen otro nombre
   (en Windows suelen ser `MYRIADPRO-REGULAR.OTF`, etc., en
   `C:\Windows\Fonts`), cópialos y renómbralos.
2. Crea una carpeta `fonts/` dentro de la carpeta de la plantilla (`actas/fonts/`
   o `documentos/fonts/`) y pon allí los cuatro archivos. En Overleaf: «New
   Folder» llamada `fonts` y sube los archivos dentro.
3. Compila con **LuaLaTeX** (o XeLaTeX).

Para comprobar que ha funcionado, abre el PDF, ve a «Propiedades → Fuentes» y
deberían aparecer `MyriadPro-Regular` y `MyriadPro-Bold`. Si aparece
`SourceSans3`, la plantilla no ha encontrado `fonts/MyriadPro-Regular.otf`.

Si compartes un proyecto de Overleaf con las fuentes dentro, que sea privado.

## Antes de firmar

Las plantillas configuran hyperref sin `/OpenAction`
(`\hypersetup{pdfstartview={}}`). Esa acción, que hyperref añade por defecto
al abrir el PDF, hace fallar la firma digital. Los enlaces normales no dan
problemas.

## Firmar

Los documentos dejan un hueco encima del nombre para la firma digital
(AutoFirma o Acrobat). Firma el PDF compilado sin la marca «BORRADOR».
