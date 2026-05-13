# Documentación de Estructura de Datos

## Base de Datos del Sistema

### Tabla 1: HABITACIONES

```
Estructura:
┌─────────────────────────────────────────────────────────────────┐
│ Habitación │ Estado │ Llaves │ Toallas │ Control │ Obs. │ Fecha │
├─────────────────────────────────────────────────────────────────┤
│     1      │ Disp   │   1    │    5    │    1    │ OK   │ 5/13  │
│     2      │ Ocup   │   0    │    3    │    1    │ OK   │ 5/13  │
│     3      │ Mant   │   1    │    2    │    0    │ TV   │ 5/13  │
│    ...     │  ...   │  ...   │   ...   │   ...   │ ...  │ ...   │
│     30     │ Disp   │   1    │    4    │    1    │ OK   │ 5/13  │
└─────────────────────────────────────────────────────────────────┘

Campos:
- Habitación #: 1-30 (Identificador único)
- Estado: Disponible | Ocupada | Mantenimiento
- Llaves: 0-2 (cantidad)
- Toallas: 0-10 (cantidad)
- Control: 0-1 (booleano)
- Observaciones: Texto libre, máx 255 caracteres
- Última Actualización: Fecha/Hora automática
```

### Tabla 2: INVENTARIO

```
Estructura:
┌──────────────────────────────────────────────────────────────┐
│ Código │ Descripción │ Almacén │ En Uso │ Baja │ Total │ Stock │
├──────────────────────────────────────────────────────────────┤
│  LLV-001  │ Llave Habitación   │   15    │   27   │   3   │   45  │ Bajo  │
│  TOA-001  │ Toalla Grande      │   50    │  120   │  10   │  180  │ OK    │
│  TOA-002  │ Toalla Pequeña     │   80    │   80   │   5   │  165  │ OK    │
│  CTR-001  │ Control Remoto     │   5     │   28   │   2   │   35  │ Bajo  │
│  ...      │ ...                │  ...    │  ...   │  ...  │  ...  │ ...   │
└──────────────────────────────────────────────────────────────┘

Campos:
- Código: Identificador único (ej: LLV-001)
- Descripción: Nombre del artículo
- En Almacén: Cantidad disponible en bodega
- En Uso: Cantidad en habitaciones
- Dados de Baja: Dañados, perdidos
- Total: =Almacén+En Uso+Baja
- Stock: Indicador visual (OK/Bajo/Crítico)

Validaciones:
- Total debe ser >= En Uso
- No se pueden ingresar negativos
- Alertas si En Almacén < 5
```

### Tabla 3: MANTENIMIENTO

```
Estructura:
┌─────────────────────────────────────────────────────────────────────┐
│ Fecha │ Habitación │ Categoría │ Descripción │ Prioridad │ Responsable │ Estado │
├─────────────────────────────────────────────────────────────────────┤
│ 5/13  │     5      │  Cuarto   │ Pared manchada│  Media    │   Juan    │ Abierto│
│ 5/13  │    12      │  Baño     │ Grifo gotea    │   Alta    │   María   │ Abierto│
│ 5/12  │     3      │  Camas    │ Sábana rota    │   Baja    │   Pedro   │ Cerr. │
│ ...   │    ...     │   ...     │     ...       │    ...    │    ...    │  ...  │
└─────────────────────────────────────────────────────────────────────┘

Campos:
- Fecha: Fecha del registro
- Habitación: 1-30
- Categoría: Cuarto|Camas|Muebles|Electrónicos|Baño|Otros
- Descripción: Detalle del problema
- Prioridad: Baja (🟢) | Media (🟡) | Alta (🔴)
- Responsable: Nombre del personal
- Estado: Abierto | En Progreso | Cerrado
- Fecha Cierre: Cuando se resuelve

Subcategorías:
- CUARTO: Pared, Puerta, Vidrios
- CAMAS: Sábanas, Frazadas, Sobresábanas
- MUEBLES: Roperos, Mesas de noche
- ELECTRÓNICOS: Teléfono, TV, Lámparas, Focos
- BAÑO: Inodoro, Lavamanos, Ducha
- OTROS: (Libre)
```

### Tabla 4: CONFIGURACIÓN

```
Parámetros del Sistema:

- Total Habitaciones: 30
- Items Críticos por Habitación: 3 (Llaves, Toallas, Control)
- Contacto Administrador: [Usuario actual]
- Fecha Inicio Sistema: [Fecha actual]
- Versión: 1.0
- Última Copia Seguridad: [Fecha]
```

## Relaciones entre Tablas

```
HABITACIONES
     │
     ├─→ INVENTARIO (items en uso)
     │
     └─→ MANTENIMIENTO (observaciones)

Flujo de Datos:
1. Se registra item en INVENTARIO
2. Se asigna a habitación en HABITACIONES
3. Se suma automáticamente a "En Uso"
4. Si hay problema → Se registra en MANTENIMIENTO
5. Al resolver → Se actualiza HABITACIONES
6. Si está dañado → Se incrementa "Dados de Baja"
```

## Fórmulas Clave

### Validaciones
```
- Estado: =IFERROR(INDEX({"Disponible";"Ocupada";"Mantenimiento"},1),"Error")
- Stock: =IF(D2<5,"Bajo",IF(D2<10,"Medio","OK"))
- Total: =B2+C2+D2
```

### Cálculos
```
- Habitaciones Disponibles: =COUNTIF(Estado,"Disponible")
- Habitaciones Ocupadas: =COUNTIF(Estado,"Ocupada")
- Habitaciones Mantenimiento: =COUNTIF(Estado,"Mantenimiento")
- Items Faltantes: =SUMIF(Stock,"Bajo",1)
- Total Inventario: =SUM(Total_Column)
```

### Reportes
```
- Reporte Diario: Filtro de fecha = HOY()
- Tareas Pendientes: Filtro Estado = "Abierto"
- Tareas por Responsable: Filtro Responsable
- Items Críticos Faltando: Filtro Llaves+Toallas+Control
```

## Validación de Datos

### Reglas de Integridad

1. **HABITACIONES**
   - Número: 1-30 (único)
   - Estado: Valores predefinidos
   - Cantidades: >= 0
   - Observaciones: Máx 255 caracteres

2. **INVENTARIO**
   - Código: Único, formato LLL-NNN
   - En Almacén >= 0
   - En Uso >= 0
   - Baja >= 0
   - Total = Almacén + En Uso + Baja

3. **MANTENIMIENTO**
   - Habitación: 1-30
   - Categoría: Valores predefinidos
   - Prioridad: Alta|Media|Baja
   - Descripción: Requerida

## Exportación de Datos

### Formatos Soportados
- Excel (.xlsx, .xlsm)
- PDF (desde reportes)
- CSV (desde tabla de datos)
- Imagen (capturas de pantalla)

### Campos Exportables
- Todas las tablas
- Reportes generados
- Gráficos
- Historial

## Seguridad y Backup

### Protección
- Protección de hoja: Sí
- Protección de celda: Fórmulas/Datos críticos
- Contraseña: Recomendada

### Backup
- Frecuencia: Diaria
- Ubicación: Carpeta de backup local
- Retención: Último mes
- Versión: Nombrada por fecha