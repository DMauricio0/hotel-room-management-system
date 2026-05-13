# 📚 Ejemplos Prácticos - Sistema de Gestión de Habitaciones

## Tabla de Contenidos

1. [Ejemplo 1: Primer Día de Operación](#ejemplo-1-primer-día-de-operación)
2. [Ejemplo 2: Habitación con Problema](#ejemplo-2-habitación-con-problema)
3. [Ejemplo 3: Control de Inventario](#ejemplo-3-control-de-inventario)
4. [Ejemplo 4: Reporte Diario](#ejemplo-4-reporte-diario)
5. [Ejemplo 5: Cambio de Estado](#ejemplo-5-cambio-de-estado)
6. [Ejemplo 6: Auditoría de Items](#ejemplo-6-auditoría-de-items)
7. [Ejemplo 7: Actualización en Masa](#ejemplo-7-actualización-en-masa)
8. [Ejemplo 8: Resolución de Problemas](#ejemplo-8-resolución-de-problemas)

---

## 📋 Ejemplo 1: Primer Día de Operación

### Escenario
Es tu primer día usando el sistema. Necesitas registrar 5 habitaciones con su estado inicial.

### Paso 1: Configuración inicial

1. Abre INICIO
2. Ve a CONFIGURACION
3. Completa:
   - Total Habitaciones: 30
   - Usuario: Tu nombre
   - Fecha Inicio: 13/05/2026

### Paso 2: Crear habitaciones iniciales

**Habitación 1:**
```
INICIO → ➕ Agregar Habitación

Número: 1
Estado: Disponible
Llaves: 2
Toallas: 10
Control: SI
Observaciones: Recién limpiada
```

**Habitación 2:**
```
Número: 2
Estado: Disponible
Llaves: 2
Toallas: 8
Control: SI
Observaciones: OK
```

**Habitación 3:**
```
Número: 3
Estado: Ocupada
Llaves: 0 (En poder del cliente)
Toallas: 5
Control: SI
Observaciones: Cliente: Sr. García
```

**Habitación 4:**
```
Número: 4
Estado: Disponible
Llaves: 1 (Falta 1 llave)
Toallas: 10
Control: SI
Observaciones: [CUARTO-PUERTA] Revisar bisagra
```

**Habitación 5:**
```
Número: 5
Estado: Mantenimiento
Llaves: 2
Toallas: 0 (Todas en lavandería)
Control: NO (Control sin funcionar)
Observaciones: [ELECTRÓNICOS-TV] No enciende
```

### Paso 3: Verificar resultados

Ve a HABITACIONES y verifica que todas aparezcan:

```
┌─────────────────────────────────────────────────────────┐
│ Hab # │ Estado        │ Llaves │ Toallas │ Control │ Obs │
├─────────────────────────────────────────────────────────┤
│  1    │ Disponible    │   2    │   10    │   SI    │ OK  │
│  2    │ Disponible    │   2    │    8    │   SI    │ OK  │
│  3    │ Ocupada       │   0    │    5    │   SI    │ SR  │
│  4    │ Disponible    │   1    │   10    │   SI    │ PU  │
│  5    │ Mantenimiento │   2    │    0    │   NO    │ TV  │
└─────────────────────────────────────────────────────────┘
```

✅ **Resultado esperado:** 
- 3 disponibles
- 1 ocupada
- 1 en mantenimiento
- Alertas visuales en items faltantes

---

## 🔧 Ejemplo 2: Habitación con Problema

### Escenario
A las 14:30 hs reciben reporte: "Habitación 5 - Grifo del baño gotea constantemente"

### Paso 1: Reportar el problema

**Opción A: Desde HABITACIONES (Rápida)**
```
1. Ve a HABITACIONES
2. Fila de Habitación 5
3. Columna "Observaciones", borra estado anterior
4. Escribe: [BAÑO-LAVAMANOS] Grifo gotea constantemente
5. Presiona Enter
```

**Opción B: Desde MANTENIMIENTO (Formal)**
```
1. Ve a MANTENIMIENTO
2. Haz clic en ➕ Nueva Tarea
3. Completa:
   - Fecha: 13/05/2026
   - Habitación: 5
   - Categoría: Baño
   - Subcategoría: Lavamanos
   - Descripción: Grifo gotea constantemente, posible pérdida de agua
   - Prioridad: 🟡 Media (no es emergencia pero debe repararse hoy)
   - Responsable: Carlos (plomero)
   - Estado: Abierto
```

### Paso 2: Verificar alertas

El sistema automáticamente:
- ✓ Marca la celda de observación en ROJO
- ✓ Alerta al personal de turno
- ✓ Incluye tarea en reporte diario

### Paso 3: Seguimiento

**14:50 hs - Carlos comienza el trabajo:**
```
MANTENIMIENTO → Busca tarea de Habitación 5
Cambia Estado: Abierto → En Progreso
```

**16:20 hs - Trabajo completado:**
```
MANTENIMIENTO → Busca tarea de Habitación 5
Actualiza:
- Estado: Cerrado
- Observación: Reemplazado grifo del lavamanos
- Fecha de Cierre: 13/05/2026
```

**En HABITACIONES:**
```
Habitación 5 - Observaciones: [BAÑO-LAVAMANOS] ✓ Reparado 13/05
```

✅ **Resultado esperado:** Problema documentado, resuelto y archivado

---

## 📦 Ejemplo 3: Control de Inventario

### Escenario
Es lunes a las 08:00 hs. Haces inventario de las toallas.

### Verificación de stock

**Paso 1: Accede a INVENTARIO**

```
INICIO → Ver Inventario
   O ve a la pestaña INVENTARIO
```

**Paso 2: Revisa el estado actual**

```
Código   │ Descripción      │ Almacén │ En Uso │ Baja │ Total │ Stock
---------|------------------|---------|--------|------|-------|--------
TOA-001  │ Toalla Grande    │   12    │  110   │  8   │  130  │ 🟡 Bajo
TOA-002  │ Toalla Pequeña   │   45    │   85   │  5   │  135  │ 🟢 OK
```

**Paso 3: Análisis**

- Toallas Grandes: Almacén = 12 → **Bajo**
  - En uso: 110 (distribuidas en 22 habitaciones x 5 toallas)
  - Recomendación: **Reordenar hoy**

- Toallas Pequeñas: Almacén = 45 → **OK**
  - En uso: 85
  - Recomendación: **Mantener**

### Realizar reorden

**Opción A: Actualizar cantidad (Si recibes toallas)**
```
INVENTARIO → TOA-001
Almacén: 12 → 50 (recibiste 38 toallas nuevas)
Guardar
```

**Opción B: Marcar como dados de baja**
```
INVENTARIO → TOA-001
Baja: 8 → 15 (encontraste 7 toallas dañadas)
Guardar
El sistema actualiza automáticamente Total y Stock
```

### Sistema de alertas

```
El sistema alerta cuando:
- 🔴 Almacén < 5  → CRÍTICO (Reordenar HOY)
- 🟡 Almacén < 10 → BAJO (Reordenar esta semana)
- 🟢 Almacén ≥ 10 → OK (Stock adecuado)
```

✅ **Resultado esperado:** 
- Stock actualizado
- Alertas automáticas
- Datos listos para orden de compra

---

## 📊 Ejemplo 4: Reporte Diario

### Escenario
Es viernes 17:00 hs. El supervisor solicita reporte del día.

### Generación automática

**Paso 1: Ve a INICIO**

```
INICIO → 📊 Generar Reporte Diario
Sistema crea automáticamente nueva hoja: REPORTE_DIARIO
```

**Paso 2: Contenido del reporte**

```
╔════════════════════════════════════════════════════╗
║    REPORTE DIARIO - VIERNES 13/05/2026           ║
║          Generado a las 17:00 hs                  ║
╠════════════════════════════════════════════════════╣
║                                                    ║
║  RESUMEN DEL DÍA:                                  ║
║  ✓ Habitaciones Disponibles: 18                   ║
║  ✓ Habitaciones Ocupadas: 10                      ║
║  ✓ Habitaciones Mantenimiento: 2                  ║
║  ✓ TOTAL: 30 habitaciones                         ║
║                                                    ║
║  ESTADO DE HABITACIONES:                           ║
║  [Tabla completa con todas las 30 habitaciones]   ║
║                                                    ║
║  INVENTARIO CRÍTICO:                              ║
║  - Toalla Grande (TOA-001): 12 unidades en stock ║
║  - Llave (LLV-001): 8 unidades en stock           ║
║  ACCIÓN: Reordenar hoy                            ║
║                                                    ║
║  TAREAS DE MANTENIMIENTO ABIERTAS:                ║
║  1. Hab 5 - Baño - Grifo gotea - Alta - Carlos   ║
║  2. Hab 8 - Cuarto - Puerta rota - Media - Juan  ║
║  3. Hab 12 - Electrónicos - TV no enciende - Baja│
║                                                    ║
║  ÁREA DE FIRMA:                                    ║
║  Supervisor: _________________ Fecha: _____       ║
║  Turno: _________________ Hora: _____             ║
║                                                    ║
╚════════════════════════════════════════════════════╝
```

### Opciones de salida

**Imprimir:**
```
INICIO → 🖨️ Imprimir
Configurar impresora y haz clic en Imprimir
```

**Exportar PDF:**
```
INICIO → 📄 Exportar PDF
Se guarda como: Reporte_13052026.pdf
```

**Archivar:**
```
Copia el reporte a carpeta: /Reportes/2026/Mayo/
```

✅ **Resultado esperado:** 
- Reporte completo y legible
- Firmado por supervisor
- Archivado para auditoría

---

## 🔄 Ejemplo 5: Cambio de Estado

### Escenario
Sábado 10:00 hs. Cliente de Habitación 3 se va. Necesitas actualizar estados.

### Proceso de checkout

**Paso 1: Cliente abandona habitación 3**

ANTES:
```
Habitación 3
Estado: Ocupada
Llaves: 0 (Cliente devuelve llaves)
Toallas: 2 (Usadas, en canasto)
Control: SI
Obs: Cliente García - CheckOut 14/05
```

**Paso 2: Actualizar en HABITACIONES**

```
INICIO → ✏️ Editar Habitación
   O ve a HABITACIONES → Fila 3

Cambios:
- Estado: Ocupada → Disponible (para limpieza)
- Llaves: 0 → 2 (Cliente devolvió)
- Toallas: 2 → 0 (Se envían a lavandería)
- Control: SI → SI
- Observaciones: [CUARTO] Requiere limpieza profunda
```

**Paso 3: Registro en inventario**

```
INVENTARIO → Automático:
Si quitamos 0 toallas de habitación, 
se restan de "En Uso" y se suman a "Almacén" (si están limpias)
O se suman a "Baja" (si están dañadas)
```

**Paso 4: Crear tarea de limpieza**

```
MANTENIMIENTO → ➕ Nueva Tarea

Fecha: 14/05/2026
Habitación: 3
Categoría: Cuarto
Descripción: Limpieza profunda post-checkout García
Prioridad: 🟡 Media (urgente hoy)
Responsable: Equipo de limpieza
Estado: Abierto
```

**Paso 5: Seguimiento**

```
10:30 hs - Limpieza iniciada
MANTENIMIENTO → Actualizar Estado: En Progreso

12:00 hs - Limpieza completada
MANTENIMIENTO → Actualizar Estado: Cerrado
HABITACIONES → Actualizar Habitación 3: Estado: Disponible
```

✅ **Resultado esperado:** 
- Habitación lista para nuevo cliente
- Inventario actualizado
- Auditoria completa del movimiento

---

## 🔍 Ejemplo 6: Auditoría de Items

### Escenario
Fin de mes. Auditoría física de llaves. Encontraste 2 llaves faltando.

### Procedimiento de auditoría

**Paso 1: Verificar registros actuales**

```
INVENTARIO → Llave (LLV-001)

Estado actual según sistema:
- En Almacén: 12
- En Uso: 25 (en habitaciones)
- Dados de Baja: 3
- TOTAL: 40
```

**Paso 2: Contar físicamente**

```
Conteo manual:
- Almacén: 12 ✓ (Coincide)
- En habitaciones: 23 (DISCREPANCIA: Faltan 2)
- Dados de baja: 3 ✓ (Coincide)
- TOTAL FÍSICO: 38 (contra 40 registrados)
```

**Paso 3: Registrar discrepancia**

```
MANTENIMIENTO → Nueva Tarea

Fecha: 31/05/2026
Categoría: Otros
Descripción: AUDITORÍA - Faltan 2 llaves. Sistema registra 25 en uso, conteo físico: 23. 
Posible pérdida o error de registro.
Prioridad: 🔴 Alta (pérdida de items)
Responsable: Supervisor
Estado: Abierto
```

**Paso 4: Corrección en sistema**

```
INVENTARIO → LLV-001
En Uso: 25 → 23 (corrección basada en conteo real)
Baja: 3 → 5 (agregar las 2 faltantes como perdidas)
Total: 40 → 38 (automático)
```

**Paso 5: Investigación**

Posibles causas:
- Llave perdida en habitación 7 (revisar)
- Llave mal registrada hace 2 semanas
- Llave dada a cliente por error

**Paso 6: Actualizar HABITACIONES**

```
Si encontraste que fue en Habitación 7:
Habitación 7 → Observaciones: [CUARTO] Llave faltante desde 5/25
Crear tarea para investigar al cliente
```

✅ **Resultado esperado:** 
- Discrepancia documentada
- Sistema corregido
- Auditoría completa archivada

---

## 📈 Ejemplo 7: Actualización en Masa

### Escenario
Llega nuevo lote de toallas. Necesitas actualizar el inventario de 150 toallas nuevas.

### Opción 1: Actualización individual

```
INVENTARIO → TOA-001
Almacén: 12 → 162 (12 + 150)
```

El sistema automáticamente:
- Recalcula Total
- Actualiza Stock a 🟢 OK
- Borra alerta de 🟡 Bajo

### Opción 2: Registro de llegada (VBA avanzado)

```
INICIO → 📦 Nueva Llegada de Inventario

Proveedor: ABC Textiles
Fecha: 14/05/2026
Referencia guía: 2026-5-12345

Items:
┌──────────────┬──────────┬──────────┐
│ Código       │ Descripción    │ Cantidad │
├──────────────┼──────────┼──────────┤
│ TOA-001      │ Toalla Gde     │ 100      │
│ TOA-002      │ Toalla Peq     │ 50       │
└──────────────┴──────────┴──────────┘

El sistema suma automáticamente a Almacén
```

### Verificación posterior

```
INVENTARIO después:

Código   │ Descripción    │ Almacén │ En Uso │ Baja │ Total │ Stock
---------|----------------|---------|--------|------|-------|--------
TOA-001  │ Toalla Grande  │  112    │  110   │  8   │ 230   │ 🟢 OK
TOA-002  │ Toalla Pequeña │   95    │   85   │  5   │ 185   │ 🟢 OK
```

✅ **Resultado esperado:** 
- Stock actualizado
- Alertas resueltas
- Documentación completa

---

## 🆘 Ejemplo 8: Resolución de Problemas

### Problema 1: "El control de Habitación 5 no aparece"

**Verificación:**
```
1. ¿Existe la Habitación 5? 
   → Ve a HABITACIONES, busca número 5
   
2. ¿El valor está registrado?
   → Columna "Control" debe tener SI o NO
   
3. ¿Hay error de validación?
   → El sistema solo acepta SI o NO
   → Revisa que hayas escrito correctamente
```

**Solución:**
```
INICIO → ✏️ Editar Habitación 5
Verifica: Control = SI
Guardar
```

---

### Problema 2: "Falta llave en Habitación 10, pero no aparece alerta"

**Verificación:**
```
HABITACIONES → Habitación 10 → Columna "Llaves"
¿Está en 0? Si no, aumenta primero la alerta.
```

**Causa probable:**
```
- La celda no está validada
- Necesitas ejecutar función VerificarEstados()
```

**Solución:**
```
Si usas VBA:
  Abre el Editor (Alt+F11)
  Ejecuta: VerificarEstados()

Si usas Fórmulas:
  Añade formato condicional a columna C:
  Si C=0 → Fondo Rojo
```

---

### Problema 3: "El reporte no se genera"

**Verificación:**
```
1. ¿Hay datos en HABITACIONES?
   → Mínimo 1 habitación debe existir
   
2. ¿Hay datos en INVENTARIO?
   → Mínimo 1 item debe existir
   
3. ¿Ya existe REPORTE_DIARIO?
   → Si existe, será reemplazado automáticamente
```

**Solución:**
```
1. Verifica haya al menos 1 habitación
2. Ve a INICIO
3. Haz clic en 📊 Generar Reporte Diario
4. Debería crear nueva hoja
5. Si falla, intenta nuevamente

Si persiste: Ejecuta → LimpiarReportesAntiguos()
```

---

### Problema 4: "No puedo editar una celda"

**Causa probable:**
```
- La hoja está protegida
- La celda está bloqueada
- Tienes permisos limitados
```

**Solución:**
```
VER → Desproteger hoja
(Puede pedir contraseña)

Si no recuerdas contraseña:
- Contacta al supervisor
- Se puede resetear en VBA
```

---

### Problema 5: "Los números aparecen como texto"

**Verificación:**
```
¿La celda tiene apóstrofe (') adelante?
Ejemplo: '0123 en lugar de 0123
```

**Solución:**
```
1. Haz clic en la celda
2. Borra el apóstrofe
3. Presiona Enter
4. Formatea como número
   Ctrl+1 → Número → OK
```

---

## 🎓 Recapitulación

Con estos 8 ejemplos prácticos aprendiste:

✅ Ejemplo 1: Configuración inicial
✅ Ejemplo 2: Reportar problemas de mantenimiento
✅ Ejemplo 3: Controlar inventario y alertas
✅ Ejemplo 4: Generar reportes diarios
✅ Ejemplo 5: Actualizar estados de habitaciones
✅ Ejemplo 6: Realizar auditorías
✅ Ejemplo 7: Actualizar datos en masa
✅ Ejemplo 8: Resolver problemas comunes

**Próximo paso:** Consulta GUIA_USO.md para profundizar en cualquier aspecto.