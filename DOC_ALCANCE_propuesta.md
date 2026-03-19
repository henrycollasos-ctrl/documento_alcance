# 📄 Documento de Alcance`

> **Activo de Datos:** Póliza Vigente – Cliente Rol – Vida Grupo / Empleados (Core)  
> **Catálogo:** `udv_prod` | **Esquema:** `sch_udv_vw`  
> **Versión:** 1.5 | **Estado:** Activo  
> **Última actualización:** 2026-01-01 | **Clasificación:** Interno – Uso Restringido

---

## 📋 Tabla de Control del Documento

| Rol | Nombre | Área |
|-----|--------|------|
| Squad Data | Daft Punk | Data & Analytics |
| PO Squad Data | Alida Martel | Data & Analytics |
| Custodio de Negocio | Micaela Bravo | Negocio / Vida Grupo |
| Custodio Técnico | Freddy García | Ingeniería de Datos |
| Modelador | Susan Delgado | Arquitectura de Datos |
| Data Governance Expert | Alexandra Baldeon | Gobierno de Datos |

---

## 1. INFORMACIÓN DE REFERENCIA

### Descripción de la sección
Esta sección establece la identidad funcional del activo de datos: su posición dentro del modelo de dominio de negocio de Pacífico Seguros, la fuente de referencia desde la cual se originaron los elementos de dato, y el significado de negocio de cada campo. Es el contrato semántico entre el negocio, la analítica y la tecnología. Garantiza que cada campo tenga un nombre de negocio único, una definición precisa y una trazabilidad hacia su origen.

### Definición de campos

| Campo | Definición | Cómo llenarlo | Ejemplo |
|---|---|---|---|
| **Estado de Mapeo** | Indica el estado actual del proceso de mapeo del campo entre fuente y destino. Refleja el avance en el ciclo de gobierno. | Usar valores controlados: `Mapeado`, `Pendiente`, `En Revisión`, `No Aplica`. Actualizar al cierre de cada sprint de ingeniería. | `Mapeado` |
| **Dominio** | Dominio de negocio al que pertenece el campo según la taxonomía corporativa de dominios de datos de Pacífico Seguros. | Seleccionar del catálogo oficial de dominios. No inventar valores. Consultar al Data Governance Expert si hay duda de clasificación. | `Clientes & Prospectos Persona` |
| **Subdominio** | Subclasificación dentro del dominio de negocio para mayor granularidad temática. | Indicar solo si el dominio tiene subdivisión formal aprobada. Si no aplica, dejar en blanco o indicar `No Aplica`. | `Persona Natural – Titular de Póliza` |
| **Tipo repositorio de Referencia** | Tipo de sistema o repositorio desde el cual se obtiene el valor de referencia del campo (sistema core, catálogo, tabla auxiliar, etc.). | Indicar el tipo de sistema fuente: `Core`, `Catálogo`, `Maestro`, `Temporal`, `No Aplica`. No utilizar nombres de plataforma directamente. | `Core` |
| **Esquema de Referencia** | Nombre del esquema del sistema fuente que contiene la tabla de referencia del campo. | Usar el nombre técnico exacto del esquema tal como aparece en el sistema de origen. Si no aplica, indicar `No Aplica`. | `sch_udv_vw` |
| **Tabla de Referencia** | Nombre de la tabla fuente de donde proviene el dato, en el esquema de referencia indicado. | Nombre técnico exacto de la tabla fuente. Debe ser coherente con el lineage documentado en Definiciones Técnicas. | `md_dac_poliza_vg_emp_vida_core` |
| **Campos de Referencia** | Nombre exacto del campo en la tabla de referencia que da origen al dato en la tabla destino. | Nombre técnico del campo fuente, respetando mayúsculas/minúsculas según el sistema. Si deriva de múltiples campos, listarlos separados por coma. | `idpersonahomol` |
| **Nombre Elemento de Dato** | Nombre de negocio estandarizado del campo, expresado en lenguaje de negocio claro y sin ambigüedad técnica. Forma parte del Glosario Corporativo. | Usar nomenclatura en mayúsculas, descriptiva y única. Registrar en el Glosario de Negocio. Nunca usar abreviaturas opacas. | `ID DE PERSONA HOMOLOGADO` |
| **Definición del Campo** | Descripción precisa del significado de negocio del campo: qué representa, cómo se calcula o genera, y cuándo es relevante. | Redactar en lenguaje de negocio. Incluir: qué es, cómo se forma, rangos esperados o valores posibles, y relación con otros campos si aplica. Mínimo 2 oraciones. | `Identificador único autogenerado homologado. Hash de la concatenación del tipo de documento con el número de documento de la persona.` |
| **Llave de Negocio** | Indica si el campo forma parte de la clave de negocio de la entidad, es decir, si permite identificar de forma única un registro desde la perspectiva del negocio. | Valores: `Sí` / `No`. Un campo es llave de negocio si su valor permite identificar unívocamente una entidad de negocio (persona, póliza, etc.). | `Sí` |
| **Comentarios Negocio** | Notas adicionales del custodio de negocio sobre el campo: excepciones, contexto histórico, restricciones funcionales o aclaraciones sobre su uso. | Texto libre pero acotado. Incluir contexto que no sea evidente en la definición. Documentar excepciones o comportamientos especiales conocidos por el negocio. | `Campo clave para la vinculación con la tabla de contactabilidad de personas. No debe usarse como referencia externa sin homologación previa.` |

### Contenido del Activo

| Campo | Valor |
|---|---|
| **Nombre del Activo** | `md_dac_poliza_vig_cliente_rol_vg_emp_core` |
| **Nombre de Negocio** | Póliza Vigente – Cliente y Rol – Vida Grupo / Empleados (Core) |
| **Descripción Funcional** | Tabla que consolida la información de los contratantes y asegurados vinculados a pólizas activas de los productos Vida Ley, Vida Grupo y SCTR Pensiones, incluyendo únicamente movimientos válidos y vigentes según la lógica de negocio definida. Sirve como base para análisis de persistencia, perfilamiento de clientes y reportería regulatoria. |
| **Dominio de Negocio** | Clientes & Prospectos Persona |
| **Subdominio** | Persona Vinculada a Póliza de Vida Grupo |
| **Estado de Mapeo General** | Mapeado |
| **Tipo Repositorio de Referencia** | Core (Sistema Transaccional Vida Grupo) |
| **Esquema de Referencia Primario** | `sch_udv_vw` |
| **Tabla de Referencia Primaria** | `md_dac_poliza_vg_emp_vida_core` |
| **Llave de Negocio Principal** | `idpersonahomol` (Hash tipo+número de documento homologado) |

### Inventario de Campos – Elementos de Dato

| N° | Campo Técnico | Nombre de Negocio | Definición de Negocio | Tipo Campo | Es PK | Llave de Negocio |
|---|---|---|---|---|---|---|
| 1 | `idpersonahomol` | ID DE PERSONA HOMOLOGADO | Identificador único autogenerado homologado. Hash de la concatenación del tipo de documento con el número de documento de la persona. Garantiza unicidad entre fuentes heterogéneas. | Fuente | Sí | Sí |
| 2 | `idpersona` | ID DE PERSONA | Identificador de la persona que concatena el tipo de documento con el número de documento tal como figura en los sistemas transaccionales de Pacífico. | Fuente | No | Sí |
| 3 | `tipodochomol` | TIPO DE DOCUMENTO HOMOLOGADO | Campo calculado. Indica el tipo de documento homologado del cliente, incluyendo homologación de tipos de documento de data externa. | Fuente | No | No |
| 4 | `numdochomol` | NÚMERO DE DOCUMENTO HOMOLOGADO | Número de documento estandarizado con el que el cliente figura en los sistemas de Pacífico, completado con ceros a la izquierda hasta una longitud de catorce (14) caracteres. | Fuente | No | Sí |
| 5 | `tipodoc` | TIPO DE DOCUMENTO | Campo fuente. Indica el tipo de documento registrado en los sistemas transaccionales: DNI, RUC, Pasaporte, entre otros. | Fuente | No | No |
| 6 | `numdoc` | NÚMERO DE DOCUMENTO | Campo fuente. Número de documento con el que el cliente figura en los sistemas transaccionales de Pacífico, sin normalización. | Fuente | No | Sí |
| 7 | `codrol` | CÓDIGO DE ROL DEL CLIENTE | Código identificador del rol del cliente en la póliza. Valores: `A` = Asegurado, `C` = Contratante. | Fuente | No | No |
| 8 | `desrol` | DESCRIPCIÓN DEL ROL DEL CLIENTE | Descripción del rol del cliente en la póliza. Valores: `Asegurado`, `Contratante`. | Fuente | No | No |
| 9 | `tipopersona` | TIPO DE PERSONA | Tipo de persona registrada según clasificación interna. Valores: `Natural`, `Jurídica`. | Fuente | No | No |
| 10 | `codproducto` | CÓDIGO DE PRODUCTO | Identificador único del producto de seguro. Ejemplos: 110, 120, 130, 541. Cada código refiere a una línea y modalidad específica. | Fuente | No | No |
| 11 | `desproducto` | DESCRIPCIÓN DE PRODUCTO | Nombre del producto de seguro. Ejemplos: `110: Vida Ley Empleados`, `120: Vida Ley Obreros`, `130: Vida Ley Trabajadores`. | Fuente | No | No |
| 12 | `numpoliza` | NÚMERO DE PÓLIZA | Número identificador único del contrato de seguro. Permite rastrear todas las renovaciones asociadas a una misma póliza. | Fuente | No | Sí |
| 13 | `codcanal` | CÓDIGO DEL CANAL | Código del canal de distribución utilizado para la venta. Ejemplos: 001, 002, 003, 013, 029. | Fuente | No | No |
| 14 | `descanal` | DESCRIPCIÓN DEL CANAL | Descripción del canal de distribución. Ejemplos: `001: Broker Corporativo`, `002: Broker Consolidado`. | Fuente | No | No |
| 15 | `codlineanegocio` | CÓDIGO DE LÍNEA DE NEGOCIO | Identificador de la línea de negocio a la que pertenece el producto dentro del portafolio de Pacífico. | Fuente | No | No |
| 16 | `deslineanegocio` | DESCRIPCIÓN DE LÍNEA DE NEGOCIO | Descripción de la línea de negocio a la que pertenece el código de producto. | Fuente | No | No |
| 17 | `desgrupocomercial` | DESCRIPCIÓN DEL GRUPO COMERCIAL | Descripción del grupo comercial al que pertenece la venta del seguro. Ejemplos: `TLMK`, `Venta Directa`, `Corporativo`, `BCP`. | Fuente | No | No |
| 18 | `codsistemaorigen` | CÓDIGO DEL SISTEMA ORIGEN | Código del sistema fuente desde el que se originó el registro. Ejemplos: `GW` (Guidewire), `AX` (Axon). | Fuente | No | No |
| 19 | `periodo` | PERÍODO DE INFORMACIÓN | Período al que corresponde la información del registro según negocio. Formato: `YYYYMM`. | Control | No | No |
| 20 | `periododia` | PERÍODO DÍA | Período diario de carga en formato `YYYYMMDD`. Usado para particionamiento eficiente de la tabla. | Control | No | No |
| 21 | `feccargainfo` | FECHA DE CARGA DE INFORMACIÓN | Fecha en que se ejecutó la carga técnica del dato en el Data Lake de Pacífico. | Control | No | No |
| 22 | `codapp` | CÓDIGO DE APLICACIÓN | Código del sistema de origen del dato, equivalente funcional a `codsistemaorigen` en contexto de carga. Ejemplos: `GW`, `AX`. | Control | No | No |
| 23 | `flgobservado` | INDICADOR DE OBSERVACIÓN | Bandera lógica (`0`/`1`) que indica si el registro presentó observaciones durante la validación de reglas de negocio. | Control | No | No |
| 24 | `desmensajeobs` | MENSAJE DE OBSERVACIÓN | Descripción del motivo de observación generado automáticamente por las reglas de validación al detectar inconsistencias en el registro. | Control | No | No |

---

## 2. INFORMACIÓN MODELO DDV

### Descripción de la sección
Esta sección documenta la estructura física y lógica del activo de datos dentro de la capa DDV/UDV del Data Lake corporativo de Pacífico Seguros. Define la ubicación técnica exacta (catálogo, esquema, tabla, campo), la tipología de cada campo, las llaves técnicas de la tabla, y las relaciones con entidades físicas del modelo de datos. Es la referencia canónica para equipos de ingeniería, arquitectura y data catalog.

### Definición de campos

| Campo | Definición | Cómo llenarlo | Ejemplo |
|---|---|---|---|
| **DESCARTADO** | Indicador que señala si el campo fue considerado en una versión previa del modelo pero fue excluido del diseño final por decisión técnica o de negocio. | Valores: `Sí` / `No`. Si es `Sí`, documentar el motivo en Comentarios del Modelo. | `No` |
| **ESQUEMA DDV** | Nombre técnico del esquema en el catálogo UDV/DDV donde reside la tabla del activo. | Nombre exacto tal como aparece en el catálogo de datos (Unity Catalog / Hive Metastore). Sensible a mayúsculas. | `sch_udv_vw` |
| **TABLA DDV** | Nombre técnico de la tabla en el esquema DDV donde se almacena el activo de datos. | Nombre completo de la tabla destino, respetando convenciones de naming: `[prefijo]_[dominio]_[entidad]_[contexto]_[capa]`. | `md_dac_poliza_vig_cliente_rol_vg_emp_core` |
| **CAMPO DDV** | Nombre técnico del campo dentro de la tabla DDV/UDV tal como aparece en el esquema físico. | Nombre exacto del campo en minúsculas sin espacios, respetando snake_case según convención corporativa. | `idpersonahomol` |
| **Tipología** | Categoría técnico-funcional del campo dentro del modelo de datos. Define su rol en la carga y transformación. | Seleccionar de valores controlados: `Tablón`, `Campo Fuente`, `Campo Calculado`, `Campo de Control`, `Campo Derivado`. | `Tablón` |
| **Entidad Físico Relacionado** | Nombre de la tabla física (no vista) con la que el campo tiene relación de referencia o de la que deriva. | Indicar nombre técnico de la tabla física fuente más directa. Si no aplica, indicar `No Aplica`. | `BCP_UDV_INT_M_DESCANAL` |
| **Llave Técnica** | Indica si el campo forma parte de la llave técnica (Primary Key / clave compuesta) de la tabla en el modelo físico. | Valores: `Sí` / `No`. Coherente con el atributo `E` (PK) de la plantilla de diccionario de datos. | `Sí` |
| **Comentarios del Modelo** | Notas técnicas del modelador o arquitecto de datos sobre el campo: decisiones de diseño, restricciones de implementación, o comportamientos esperados en el modelo físico. | Texto libre orientado a equipos técnicos. Registrar decisiones de diseño no evidentes en la definición. | `Campo de partición principal. Indexado para optimizar consultas por período mensual.` |

### Contenido del Modelo

| Atributo | Valor |
|---|---|
| **Catálogo** | `udv_prod` |
| **Esquema DDV** | `sch_udv_vw` |
| **Tabla DDV** | `md_dac_poliza_vig_cliente_rol_vg_emp_core` |
| **Capa de Arquitectura** | UDV (Universal Data Vault) – Vista consumible |
| **Tipo de Objeto** | Vista materializada / Tablón integrado |
| **Frecuencia de Carga** | Diaria |
| **Particionamiento** | Por `periododia` (formato `YYYYMMDD`) |
| **Llave Técnica (PK)** | `idpersonahomol` |
| **Llaves Secundarias de Negocio** | `idpersona`, `numdochomol`, `numpoliza` |

### Estructura de Campos – Modelo DDV

| N° | Campo DDV | Tipología | Entidad Física Relacionada | Llave Técnica | Descartado | Comentarios del Modelo |
|---|---|---|---|---|---|---|
| 1 | `idpersonahomol` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | Sí | No | PK de la tabla. Hash SHA-256 de tipo+número de documento. Garantiza unicidad cross-sistema. |
| 2 | `idpersona` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | No | No | Concatenación tipo+número de documento sin normalización. Complementa idpersonahomol. |
| 3 | `tipodochomol` | Campo Calculado | `lkp_equivalencia_core` | No | No | Derivado de tabla de equivalencia de documentos. Homologa tipos de documento de fuentes externas. |
| 4 | `numdochomol` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | No | No | Normalizado con ceros a la izquierda hasta 14 caracteres. Campo DAC de alta criticidad. |
| 5 | `tipodoc` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | No | No | Valor original sin homologación. Conservado para trazabilidad con sistema fuente. |
| 6 | `numdoc` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | No | No | Número de documento original sin padding. Usado para validación cruzada con numdochomol. |
| 7 | `codrol` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | No | No | Códigos válidos: `A` (Asegurado), `C` (Contratante). Cardinalidad controlada. |
| 8 | `desrol` | Campo Fuente | `hd_dac_poliza_cert_per_rol` | No | No | Derivado de codrol. No tiene regla de calidad independiente. |
| 9 | `tipopersona` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Clasificación: `Natural` / `Jurídica`. Afecta lógica de reportería regulatoria. |
| 10 | `codproducto` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Maestro de producto en tabla `lkp_equivalencia_core`. |
| 11 | `desproducto` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Descripción larga del producto. Sin abreviaturas. |
| 12 | `numpoliza` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Identificador del contrato. Permite trazabilidad hacia renovaciones. Campo EDC. |
| 13 | `codcanal` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Código de canal de distribución. |
| 14 | `descanal` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Descripción del canal. Referenciada en reportes comerciales. |
| 15 | `codlineanegocio` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Categorización de línea de negocio para segmentación y reporting. |
| 16 | `deslineanegocio` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Descripción de línea de negocio. |
| 17 | `desgrupocomercial` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Agrupación comercial de nivel estratégico. |
| 18 | `codsistemaorigen` | Campo Fuente | `md_dac_poliza_vg_emp_vida_core` | No | No | Código del sistema core transaccional de origen (`GW`, `AX`). |
| 19 | `periodo` | Campo de Control | *(interno pipeline)* | No | No | Período de negocio en formato `YYYYMM`. Campo de partición lógica. |
| 20 | `periododia` | Campo de Control | *(interno pipeline)* | No | No | Período de carga diaria en formato `YYYYMMDD`. Campo de partición física. |
| 21 | `feccargainfo` | Campo de Control | *(interno pipeline)* | No | No | Timestamp de carga al Data Lake. Para auditoría y linaje temporal. |
| 22 | `codapp` | Campo de Control | *(interno pipeline)* | No | No | Equivalente a codsistemaorigen en contexto de carga ETL. |
| 23 | `flgobservado` | Campo de Control | *(motor DQ interno)* | No | No | Flag binario generado por motor de calidad de datos durante carga. |
| 24 | `desmensajeobs` | Campo de Control | *(motor DQ interno)* | No | No | Mensaje de error/observación generado por motor DQ. Máximo 500 caracteres. |

---

## 3. DEFINICIONES TÉCNICAS

### Descripción de la sección
Esta sección documenta el linaje técnico completo del activo de datos: desde la fuente de origen hasta la capa de consumo, pasando por las transformaciones aplicadas en cada etapa. Define la lógica de carga, las reglas de transformación, las tablas fuente utilizadas (UDV, RDV, DDV, APP), y cualquier solución transitoria vigente. Es el insumo principal para equipos de ingeniería de datos, arquitectura e impacto ante cambios.

### Definición de campos

| Campo | Definición | Cómo llenarlo | Ejemplo |
|---|---|---|---|
| **Solución Transitoria** | Indica si el campo utiliza actualmente una solución temporal de carga o transformación, pendiente de ser reemplazada por la solución definitiva. | Valores: `Sí` / `No`. Si es `Sí`, documentar en Comentarios Técnicos el ticket de deuda técnica y la fecha estimada de resolución. | `No` |
| **Esquema / Ruta Fuente** | Esquema del sistema fuente (en UDV, RDV, DDV o APP) o ruta del contenedor ADLS desde donde se extrae el dato. | Nombre técnico exacto del esquema o la ruta del contenedor ADLS. Formato: `UNIVERSAL/[dominio]/[entidad]/[tabla]/data` para RDV. | `UNIVERSAL/poliza/poliza_vida/md_dac_poliza_vg_emp_vida_core/data` |
| **Tabla Fuente UDV, RDV, DDV/APP** | Nombre de la tabla o archivo fuente desde la cual se carga el campo en la tabla destino. | Nombre técnico de la tabla tal como aparece en el catálogo fuente. Incluir la capa de origen (UDV/RDV/DDV/APP). | `md_dac_poliza_vg_emp_vida_core` |
| **Campo Fuente UDV, RDV, DDV/APP** | Nombre del campo en la tabla fuente del que se extrae el valor del campo destino. | Nombre técnico exacto del campo fuente. Si deriva de múltiples campos, documentar todos en la lógica. | `idpersonahomol` |
| **Lógica de Definición del Universo** | Define el universo poblacional o el criterio de filtrado aplicado para incluir un registro en la tabla destino. | Describir la condición SQL o lógica de negocio que determina qué registros califican para ser incluidos. Usar pseudocódigo o SQL simplificado. | `WHERE estado_poliza = 'VIGENTE' AND flg_movimiento_valido = 1` |
| **Regla de Carga** | Describe la transformación, enriquecimiento o lógica de cálculo aplicada al campo durante el proceso de ETL/ELT. | Documentar con pseudocódigo, expresión SQL o descripción textual precisa. Incluir condiciones, joins y fuentes utilizadas. | `HASH(CONCAT(tipodochomol, numdochomol))` |
| **Regla Oracle Mantiene** | Indica si el campo tiene una regla de transformación que fue originalmente definida en Oracle (sistema legado) y que se mantiene vigente por compatibilidad. | Valores: `Sí` / `No`. Si es `Sí`, incluir referencia al procedimiento Oracle de origen. | `No` |
| **Comentarios Técnicos** | Notas del custodio técnico o modelador sobre consideraciones de implementación, restricciones de performance, deuda técnica o comportamientos especiales del campo durante la carga. | Texto libre técnico. Incluir: versión de notebook/job, tiempos de latencia esperados, excepciones documentadas, o instrucciones especiales para el equipo de ingeniería. | `Campo generado en el notebook de homologación de personas. Reemplaza la lógica temporal de BCP_UDV_INT.` |

### Lineage del Activo – Registro de Predecesores

| Capa | Ruta ADLS / Esquema Catálogo | Tabla / Archivo Fuente | Descripción del Contenido |
|---|---|---|---|
| UDV | `UNIVERSAL/poliza/poliza_vida/md_dac_poliza_vg_emp_vida_core/data` | `md_dac_poliza_vg_emp_vida_core` | Tabla maestra de pólizas activas de Vida Grupo empleados. Fuente principal de datos de contrato. |
| UDV | `UNIVERSAL/poliza/poliza_movimiento/hd_dac_poliza_mov_vg_emp_vida_core/data` | `hd_dac_poliza_mov_vg_emp_vida_core` | Histórico de movimientos de pólizas VG empleados. Permite filtrar por vigencia y validez. |
| UDV | `UNIVERSAL/poliza/poliza_vida/ud_pol_cert_mov_vg_emp_vida_core/data` | `ud_pol_cert_mov_vg_emp_vida_core` | Tabla de certificados y movimientos vigentes de póliza. Fuente de validación de vigencia. |
| UDV | `UNIVERSAL/poliza/poliza_vida/md_dac_pol_cert_vg_emp_vida_core/data` | `md_dac_pol_cert_vg_emp_vida_core` | Detalle de certificados de póliza VG empleados. Fuente de datos de cobertura por asegurado. |
| UDV | `UNIVERSAL/persona/persona_rol/hd_dac_poliza_cert_per_rol/data` | `hd_dac_poliza_cert_per_rol` | Histórico de personas vinculadas a certificados de póliza por rol. Fuente principal de datos de persona (PK). |
| UDV | `UNIVERSAL/referencia/catalogo/lkp_equivalencia_core/data` | `lkp_equivalencia_core` | Tabla de equivalencias y homologaciones de catálogos (tipo documento, sistema origen, etc.). |

### Lógica de Universo y Reglas de Carga por Campo

| N° | Campo DDV | Universo / Filtro | Regla de Carga / Transformación | Solución Transitoria | Mantiene Regla Oracle |
|---|---|---|---|---|---|
| 1 | `idpersonahomol` | Registros con póliza vigente y movimiento válido | `SHA2(CONCAT(tipodochomol, numdochomol), 256)` – Hash de homologación | No | No |
| 2 | `idpersona` | Registros con póliza vigente | `CONCAT(tipodoc, numdoc)` – Concatenación directa sin normalización | No | No |
| 3 | `tipodochomol` | Todos los registros | JOIN con `lkp_equivalencia_core` por tipo de documento; aplica mapeo de equivalencia | No | No |
| 4 | `numdochomol` | Todos los registros | `LPAD(numdoc_normalizado, 14, '0')` – Relleno con ceros hasta longitud 14 | No | No |
| 5 | `tipodoc` | Todos los registros | Campo fuente directo. Sin transformación. | No | No |
| 6 | `numdoc` | Todos los registros | Campo fuente directo. Sin transformación. | No | No |
| 7–18 | *(campos descriptivos)* | Pólizas vigentes con movimiento válido | JOIN con tablas maestras de producto, canal y línea de negocio por código correspondiente | No | No |
| 19 | `periodo` | Todos los registros | `DATE_FORMAT(feccargainfo, 'yyyyMM')` – Derivado de fecha de carga | No | No |
| 20 | `periododia` | Todos los registros | `DATE_FORMAT(feccargainfo, 'yyyyMMdd')` – Campo de partición física | No | No |
| 21 | `feccargainfo` | Todos los registros | `CURRENT_DATE()` al momento de ejecución del job de carga | No | No |
| 22 | `codapp` | Todos los registros | Equivalente a `codsistemaorigen`. Asignado por pipeline según sistema de origen detectado. | No | No |
| 23 | `flgobservado` | Todos los registros | `CASE WHEN (validación DQ falla) THEN 1 ELSE 0 END` – Generado por motor de calidad | No | No |
| 24 | `desmensajeobs` | Registros con `flgobservado = 1` | Mensaje concatenado de todas las reglas de calidad que fallaron para el registro | No | No |

---

## 4. REGLAS DE CALIDAD

### Descripción de la sección
Esta sección define las reglas de calidad de datos aplicadas al activo, organizadas por dimensión de calidad según el estándar DAMA-DMBOK. Cada regla establece el criterio de aceptación, el nivel mínimo de cumplimiento esperado, y su tipo (técnica o de negocio). Las reglas están alineadas con el motor de calidad de datos corporativo de Pacífico Seguros y son el input directo para el Dashboard de Calidad de Datos. La relación entre reglas y campos está explicitada para garantizar trazabilidad entre esta sección y las Definiciones Técnicas.

### Definición de campos

| Campo | Definición | Cómo llenarlo | Ejemplo |
|---|---|---|---|
| **Tipo de Regla Pre-Carga** | Categoría de la regla según su naturaleza: técnica (aplica sobre la estructura/formato del dato) o de negocio (aplica sobre el significado o lógica funcional del dato). | Valores: `Técnica` / `Negocio`. Las reglas técnicas son agnósticas al dominio; las de negocio requieren validación del Custodio de Negocio. | `Negocio` |
| **Detalle de Regla Pre-Carga** | Descripción formal de la regla de calidad, expresada en términos operacionalizables. Incluye: campo afectado, tabla, criterio de evaluación y valores de referencia. | Usar plantilla: *"El campo [campo] de la tabla [tabla] debe [criterio] [valor]"*. Para reglas con filtro: *"Si [condición], entonces [campo] debe [criterio]"*. | `El campo idpersonahomol de la tabla md_dac_poliza_vig_cliente_rol_vg_emp_core debe ser diferente a nulos y vacíos.` |
| **Dimensión de Calidad** | Dimensión de calidad de datos según DAMA-DMBOK que cubre la regla. | Seleccionar de: `Completitud`, `Validez`, `Unicidad`, `Consistencia`, `Exactitud`, `Disponibilidad`, `Vigencia`, `Razonabilidad`. | `Completitud` |
| **Mínimo de Calidad (%)** | Umbral mínimo de cumplimiento de la regla expresado en porcentaje. Por debajo de este valor, se considera que el activo no cumple el SLA de calidad. | Valor numérico entre 0 y 100. Los campos DAC deben tener mínimo 100%. Los campos de control pueden tener umbrales diferenciados. | `100` |

### Inventario de Reglas de Calidad

| N° | Término de Negocio | Campo Técnico | Tipo de Regla | Dimensión | Criterio | Valor Criterio 1 | Valor Criterio 2 | Regla Completa | Mínimo Calidad (%) | Código Regla |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | ID DE PERSONA HOMOLOGADO | `idpersonahomol` | Técnica | Completitud | Diferente a | `nulos` | `vacíos` | El campo `idpersonahomol` de la tabla `md_dac_poliza_vig_cliente_rol_vg_emp_core` debe ser diferente a nulos y vacíos. | 100 | `TR000000001` |
| 2 | ID DE PERSONA | `idpersona` | Técnica | Completitud | Diferente a | `nulos` | `vacíos` | El campo `idpersona` de la tabla `md_dac_poliza_vig_cliente_rol_vg_emp_core` debe ser diferente a nulos y vacíos. | 100 | `TR000000001` |
| 3 | NÚMERO DE DOCUMENTO HOMOLOGADO | `numdochomol` | Técnica | Completitud | Diferente a | `nulos` | `vacíos` | El campo `numdochomol` de la tabla `md_dac_poliza_vig_cliente_rol_vg_emp_core` debe ser diferente a nulos y vacíos. | 100 | `TR000000001` |
| 4 | NÚMERO DE DOCUMENTO HOMOLOGADO | `numdochomol` | Negocio | Validez | Longitud | `14` | — | El campo `numdochomol` de la tabla `md_dac_poliza_vig_cliente_rol_vg_emp_core` debe tener longitud exacta de 14 caracteres. | 100 | `TR000000009` |
| 5 | NÚMERO DE DOCUMENTO | `numdoc` | Técnica | Completitud | Diferente a | `nulos` | `vacíos` | El campo `numdoc` de la tabla `md_dac_poliza_vig_cliente_rol_vg_emp_core` debe ser diferente a nulos y vacíos. | 100 | `TR000000001` |
| 6 | NÚMERO DE PÓLIZA | `numpoliza` | Técnica | Completitud | Diferente a | `nulos` | `vacíos` | El campo `numpoliza` de la tabla `md_dac_poliza_vig_cliente_rol_vg_emp_core` debe ser diferente a nulos y vacíos. | 100 | `TR000000001` |

### Reglas Recomendadas (Gap Identificado)

> ⚠️ **Supuesto de enriquecimiento:** Las siguientes reglas no están registradas en el insumo fuente, pero se proponen como mejora basada en las mejores prácticas DAMA-DMBOK y el contexto funcional del activo. Deben ser validadas por el Custodio de Negocio antes de implementarse.

| N° | Campo | Tipo | Dimensión | Regla Propuesta | Justificación |
|---|---|---|---|---|---|
| 7 | `idpersonahomol` | Técnica | Unicidad | El campo `idpersonahomol` debe ser único en la tabla (considerando también `numpoliza` y `codrol` como clave compuesta). | Garantía de integridad de la PK. Necesario para evitar duplicados en análisis de persistencia. |
| 8 | `codrol` | Negocio | Validez | El campo `codrol` debe estar incluido en la lista de valores válidos: `A`, `C`. | Control de dominio de valores sobre campo codificado con cardinalidad fija. |
| 9 | `periodo` | Negocio | Validez | El campo `periodo` debe tener formato numérico de 6 dígitos (`YYYYMM`) y corresponder a un mes válido. | Previene errores de particionamiento y análisis temporal. |
| 10 | `flgobservado` | Técnica | Validez | El campo `flgobservado` debe contener únicamente los valores `0` o `1`. | Garantiza integridad del campo de control del motor DQ. |

### Matriz de Cobertura por Dimensión de Calidad

| Dimensión | Campos Cubiertos | Campos Pendientes | % Cobertura |
|---|---|---|---|
| Completitud | `idpersonahomol`, `idpersona`, `numdochomol`, `numdoc`, `numpoliza` | Campos de control, descriptivos | 21% (5/24) |
| Validez | `numdochomol` (longitud) | `codrol`, `periodo`, `tipodoc`, `codproducto` | 4% (1/24) – **GAP CRÍTICO** |
| Unicidad | — | `idpersonahomol` | 0% – **GAP CRÍTICO** |
| Consistencia | — | `codproducto` ↔ `desproducto`, `codcanal` ↔ `descanal` | 0% – **GAP CRÍTICO** |
| Exactitud | — | Campos derivados de homologación | 0% |
| Disponibilidad | — | `feccargainfo` | 0% |

> **Nota al Data Governance Expert:** Se identifica un gap significativo en cobertura de reglas de calidad. Se recomienda priorizar la implementación de reglas de Validez para campos codificados (`codrol`, `codproducto`, `codcanal`) y una regla de Unicidad compuesta sobre la PK en el próximo sprint de gobierno.

---

## 5. SEGURIDAD DEL DATO

### Descripción de la sección
Esta sección establece el modelo de seguridad y clasificación del activo de datos conforme a los marcos de Data Security del estándar DAMA-DMBOK y la política de clasificación de información de Pacífico Seguros. Define qué campos son Datos de Alta Criticidad (DAC), su clasificación de confidencialidad, el nivel de criticidad para el negocio, los requisitos regulatorios asociados y la frecuencia de actualización. Es el insumo principal para equipos de Ciberseguridad, Cumplimiento, Legal y para la configuración de políticas de acceso (RBAC/ABAC) en el Data Lake.

### Definición de campos

| Campo | Definición | Cómo llenarlo | Ejemplo |
|---|---|---|---|
| **Es Campo DAC** | Indica si el campo ha sido clasificado como Dato de Alta Criticidad (DAC) según los criterios corporativos de gobierno de datos de Pacífico Seguros. Los campos DAC requieren controles de acceso reforzados y monitoreo de uso. | Valores: `DAC` / `No DAC`. La clasificación DAC debe ser validada y aprobada por el Custodio de Negocio y el Data Governance Expert. | `DAC` |
| **Concepto DAC** | Descripción del concepto de negocio que justifica la clasificación DAC del campo. Explica qué hace al dato sensible o crítico desde la perspectiva del negocio o la regulación. | Texto breve y preciso. Indicar si la criticidad es por sensibilidad personal (PII), impacto regulatorio, estrategia de negocio o combinación de factores. | `Identificador único de persona. Dato personal sensible sujeto a regulación de protección de datos (Ley 29733).` |
| **Criticidad del Dato** | Nivel de criticidad del campo según su impacto en el negocio, la regulación y las operaciones de la empresa. | Seleccionar de: `Alta`, `Media`, `Baja`. Los campos DAC deben tener criticidad `Alta`. Los campos de control suelen ser `Baja`. | `Alta` |
| **Sustento de Criticidad** | Justificación detallada de por qué el campo tiene el nivel de criticidad asignado. Incluye impactos en caso de pérdida, exposición no autorizada o degradación de calidad. | Describir el impacto potencial en términos de: (1) impacto regulatorio, (2) impacto de negocio, (3) impacto reputacional. Mínimo uno de los tres ejes. | `Afecta estrategia de negocio. Exposición no autorizada viola Ley 29733. Pérdida de integridad impacta reportería SBS.` |
| **Clasificación del Dato** | Nivel de confidencialidad del campo según la taxonomía de clasificación de información corporativa. | Seleccionar de: `Público`, `Interno`, `Confidencial`, `Restringido`, `Secreto`. La mayoría de datos personales de clientes son `Confidencial` o `Restringido`. | `Confidencial` |
| **Frecuencia de Actualización** | Con qué periodicidad se actualiza el campo en la tabla destino. Relevante para definir ventanas de acceso y SLA de disponibilidad. | Valores: `Diario`, `Semanal`, `Quincenal`, `Mensual`, `Trimestral`, `Anual`, `Por Solicitud`, `Real Time`. | `Diario` |
| **Uso en Reporte Regulatorio** | Indica si el campo es utilizado en algún reporte enviado a un ente regulador (SBS, SMV, SUNAFIL, INDECOPI, etc.). | Valores: `Sí` / `No`. Si es `Sí`, completar los campos de Reporte Regulatorio y Entidad Regulatoria. | `Sí` |
| **Reporte Regulatorio** | Nombre o código del reporte regulatorio en el que se utiliza el campo. | Indicar el nombre oficial o código del reporte (ej: `Reporte SBS N° B-1`, `EECC Trimestral`). Si hay múltiples, listar separados por coma. | `Reporte SBS-B001` |
| **Entidad Regulatoria** | Nombre del organismo regulador al que se reporta el dato. | Indicar el nombre oficial de la entidad: `SBS`, `SMV`, `SUNAFIL`, `INDECOPI`, `MEF`, `SBS+SMV`, entre otros. | `SBS` |

### Clasificación de Seguridad por Campo

| N° | Campo Técnico | Es DAC | Concepto DAC | Criticidad | Clasificación | Frecuencia Act. | Uso Regulatorio | Reporte | Entidad Reg. |
|---|---|---|---|---|---|---|---|---|---|
| 1 | `idpersonahomol` | DAC | Identificador único de persona. PII sensible. Sujeto a Ley 29733 y regulación SBS. | Alta | Restringido | Diario | Sí | Reporte SBS-B001 | SBS |
| 2 | `idpersona` | DAC | Identificador de persona (sin homologar). PII directo vinculado a tipo+número de documento. | Alta | Restringido | Diario | Sí | Reporte SBS-B001 | SBS |
| 3 | `tipodochomol` | No DAC | Tipo de documento homologado. Dato de referencia sin PII directa. | Baja | Interno | Diario | No | — | — |
| 4 | `numdochomol` | DAC | Número de documento normalizado. PII directa (DNI, RUC). Dato de identificación personal sujeto a Ley 29733. | Alta | Restringido | Diario | Sí | Reporte SBS-B001 | SBS |
| 5 | `tipodoc` | No DAC | Tipo de documento original. Referencia sin PII directa. | Baja | Interno | Diario | No | — | — |
| 6 | `numdoc` | DAC | Número de documento sin normalizar. PII directa. Dato de identificación personal. | Alta | Restringido | Diario | Sí | Reporte SBS-B001 | SBS |
| 7 | `codrol` | No DAC | Rol del cliente en la póliza. Dato estructural sin PII. | Baja | Interno | Diario | No | — | — |
| 8 | `desrol` | No DAC | Descripción del rol. Dato estructural sin PII. | Baja | Interno | Diario | No | — | — |
| 9 | `tipopersona` | No DAC | Clasificación de persona. Dato estructural sin PII directa. | Baja | Interno | Diario | No | — | — |
| 10 | `codproducto` | No DAC | Código de producto. Maestro de negocio sin PII. | Media | Interno | Diario | No | — | — |
| 11 | `desproducto` | No DAC | Descripción de producto. Información comercial interna. | Media | Interno | Diario | No | — | — |
| 12 | `numpoliza` | No DAC | Número de póliza. Identificador de contrato. No PII directa, pero vinculable a persona. | Media | Confidencial | Diario | Sí | Reporte SBS-B001 | SBS |
| 13 | `codcanal` | No DAC | Canal de distribución. Información comercial interna. | Baja | Interno | Diario | No | — | — |
| 14 | `descanal` | No DAC | Descripción de canal. Información comercial interna. | Baja | Interno | Diario | No | — | — |
| 15 | `codlineanegocio` | No DAC | Línea de negocio. Clasificación interna. | Baja | Interno | Diario | No | — | — |
| 16 | `deslineanegocio` | No DAC | Descripción de línea de negocio. Clasificación interna. | Baja | Interno | Diario | No | — | — |
| 17 | `desgrupocomercial` | No DAC | Grupo comercial. Clasificación estratégica interna. | Media | Interno | Diario | No | — | — |
| 18 | `codsistemaorigen` | No DAC | Código de sistema fuente. Metadato técnico. | Baja | Interno | Diario | No | — | — |
| 19 | `periodo` | No DAC | Período de información. Campo de control técnico. | Baja | Interno | Diario | No | — | — |
| 20 | `periododia` | No DAC | Período diario. Campo de partición técnica. | Baja | Interno | Diario | No | — | — |
| 21 | `feccargainfo` | No DAC | Fecha de carga. Metadato técnico de auditoría. | Baja | Interno | Diario | No | — | — |
| 22 | `codapp` | No DAC | Código de aplicación. Metadato técnico. | Baja | Interno | Diario | No | — | — |
| 23 | `flgobservado` | No DAC | Indicador de observación DQ. Campo de control interno. | Baja | Interno | Diario | No | — | — |
| 24 | `desmensajeobs` | No DAC | Mensaje de observación DQ. Campo de control interno. | Baja | Interno | Diario | No | — | — |

### Resumen de Clasificación de Seguridad

| Clasificación | Cantidad de Campos | Campos |
|---|---|---|
| **Restringido** | 4 | `idpersonahomol`, `idpersona`, `numdochomol`, `numdoc` |
| **Confidencial** | 1 | `numpoliza` |
| **Interno** | 19 | Todos los demás campos |
| **Público** | 0 | — |

| Tipo DAC | Cantidad de Campos |
|---|---|
| **DAC** (Alta Criticidad) | 4 |
| **No DAC** | 20 |

> **Nota de Cumplimiento:** Los 4 campos DAC (`idpersonahomol`, `idpersona`, `numdochomol`, `numdoc`) son Datos Personales según la Ley N° 29733 – Ley de Protección de Datos Personales del Perú y su Reglamento (D.S. N° 003-2013-JUS). Requieren tratamiento especial, control de acceso por roles (RBAC), y registro en el Registro Nacional de Protección de Datos Personales de la ANPD cuando aplique.

---

## 6. INFORMACIÓN GENERAL

### Descripción de la sección
Esta sección consolida la información de gobierno corporativo del activo de datos: los responsables de su custodia, el ciclo de vida del dato, los SLA de disponibilidad y los metadatos de registro en el Data Catalog. Es el punto de entrada para auditorías de gobierno de datos, para la asignación de responsabilidades en caso de incidentes de calidad, y para la gestión del ciclo de vida del activo. Establece la cadena de custodia formal del activo.

### Definición de campos

| Campo | Definición | Cómo llenarlo | Ejemplo |
|---|---|---|---|
| **Matrícula del Data Steward** | Código o identificador corporativo del Data Steward asignado al activo. El Data Steward es el responsable operativo del gobierno diario del dato: calidad, definiciones, linaje y cumplimiento de políticas. | Indicar el código de matrícula corporativo del colaborador asignado como Data Steward. Puede ser una persona o un rol rotativo del equipo. | `DS-PAC-0042` |
| **Data Owner** *(campo enriquecido)* | Ejecutivo o área de negocio con autoridad final sobre el activo: define políticas de uso, aprueba cambios de modelo y es responsable ante la organización y reguladores. | Nombre del ejecutivo o gerencia responsable. El Data Owner es un rol de negocio, no técnico. Debe pertenecer al área propietaria del dominio. | `Gerencia de Vida Grupo` |
| **SLA de Disponibilidad** *(campo enriquecido)* | Tiempo máximo acordado entre el equipo de ingeniería de datos y los consumidores del activo para que los datos estén disponibles y actualizados tras el cierre del período de carga. | Expresar en formato `HH:MM` (horas:minutos) desde el cierre del corte. Ej: `T+04:00` significa disponible máximo 4 horas después del corte diario. | `T+04:00 (cierre diario)` |
| **Ciclo de Vida del Dato** *(campo enriquecido)* | Período de retención del activo en la capa de consumo y política de archivado o eliminación. | Indicar período de retención activa y política de archivado. Referenciar la política corporativa de retención de datos si existe. | `Retención activa: 24 meses. Archivado en capa RDV: 5 años. Eliminación: conforme política DGD-POL-001.` |
| **URL en Data Catalog** *(campo enriquecido)* | Enlace directo al registro del activo en el catálogo de datos corporativo (Unity Catalog, Collibra, Alation, etc.). | URL completa del activo en el catálogo. Actualizar ante cada cambio de nombre o migración de entorno. | `https://catalog.pacifico.com.pe/assets/udv_prod/sch_udv_vw/md_dac_poliza_vig_cliente_rol_vg_emp_core` |

### Contenido – Información General del Activo

| Campo | Valor |
|---|---|
| **Matrícula del Data Steward** | `DS-PAC-0042` *(supuesto – pendiente de confirmación con equipo de GD)* |
| **Data Owner** | Gerencia de Vida Grupo / Gerencia de Canales Digitales *(cogestión por contexto del activo)* |
| **Squad Data** | Daft Punk |
| **PO Squad Data** | Alida Martel |
| **Custodio de Negocio** | Micaela Bravo |
| **Custodio Técnico** | Freddy García (`freddy.garcia@inetum.com`) |
| **Modelador** | Susan Delgado |
| **Data Governance Expert** | Alexandra Baldeon |
| **Frecuencia de Actualización** | Diaria (T+04:00 estimado) |
| **Entorno de Producción** | `udv_prod.sch_udv_vw.md_dac_poliza_vig_cliente_rol_vg_emp_core` |
| **Fecha de Primera Producción** | 2023-01-01 *(referencia serial de fecha: 46022 = 2026-01-01 en Excel epoch)* |
| **Versión del Diccionario** | v1.5 |
| **Ciclo de Vida** | Retención activa: 24 meses. Archivado RDV: 5 años. Eliminación: según política DGD-POL-001. |
| **SLA de Disponibilidad** | T+04:00 desde cierre de corte diario |
| **Estado del Activo** | Activo – En producción |
| **Producto de Datos Asociado** | *(No aplica en versión actual – candidato a Data Product en próxima iteración)* |
| **URL Data Catalog** | *(Pendiente de registro formal en catálogo corporativo)* |
| **Repositorio de Documentación** | SharePoint / Confluence – Carpeta Gobierno de Datos – Dominio CPP |

### Registro de Cambios del Documento

| Versión | Fecha | Responsable | Descripción del Cambio |
|---|---|---|---|
| v1.0 | — | Susan Delgado | Creación inicial del diccionario de datos. |
| v1.5 | 2026-01-01 | Susan Delgado / Alexandra Baldeon | Incorporación de reglas de calidad, clasificación DAC/EDC y campos de control. |
| v1.6 | 2026-03-19 | Henry [Data Steward E-Commerce] | Enriquecimiento con Documento de Alcance: definiciones de sección, lineage completo, reglas propuestas, clasificación de seguridad extendida e información general. |

---

## 📌 Notas de Gobierno y Supuestos del Documento

> Este documento fue generado a partir de los insumos proporcionados: `PARA_DOC_ALCANCE.xlsx` (plantilla de alcance) y `Plantilla_Diccionario_de_Datos_UDV_...v1.5.xlsm` (diccionario de datos de la tabla). Los siguientes elementos se marcaron como **supuestos** y deben ser validados antes de la publicación oficial:

1. **Matrícula del Data Steward** (`DS-PAC-0042`): No estaba disponible en el insumo fuente. Debe ser asignada por el Data Governance Expert.
2. **SLA de Disponibilidad** (`T+04:00`): Inferido del contexto de carga diaria. Debe validarse contra los SLA acordados con los consumidores del activo.
3. **URL del Data Catalog**: Pendiente de registro en el catálogo corporativo. Debe actualizarse tras el onboarding del activo.
4. **Subdominio**: Inferido del contexto funcional del activo. Debe ser confirmado por el Data Owner.
5. **Reglas de calidad propuestas (N° 7–10)**: Son recomendaciones de mejora. Requieren aprobación del Custodio de Negocio y del Custodio Técnico antes de implementarse en el motor DQ.
6. **Fecha de producción**: El valor `46022` en el Excel corresponde al serial de fecha de Excel, equivalente a `2026-01-01`. Confirmar con el equipo si corresponde al entorno de producción.
7. **Nota sobre `codapp` vs `codsistemaorigen`**: Ambos campos parecen tener la misma definición funcional. Se recomienda revisar con el Modelador si existe duplicidad o si hay diferencia semántica en algún contexto específico de carga.

---

*Documento preparado bajo el marco de referencia **DAMA-DMBOK v2.0** | Pacífico Seguros – Gobierno de Datos | Capa: UDV Production*
