# 🛠️ Manual Técnico · Barbería

**Stack:** HTML5, Tailwind CSS (CDN), Vanilla JavaScript (ES6+), LocalStorage, Cloudflare Worker / JSONBin Cloud API, QRCode.js, Canvas Confetti.  
**Despliegue:** GitHub Pages (`https://juancdgo.github.io/barberia/`).  
**Copia de Seguridad:** Google Drive / LocalStorage JSON.

---

## 1. Arquitectura del Sistema

La aplicación está diseñada como una **Single-Page Application (SPA)** de alto rendimiento, optimizada para dispositivos móviles y entornos de salón/barbería:
* Cero frameworks reactivos pesados (React/Angular/Vue no requeridos).
* Render reactivo eficiente mediante funciones puras de DOM manipulation.
* Sistema de sincronización de turnos en tiempo real mediante API REST liviana.

### Estructura del Repositorio:
```text
Mini Apps/barberia/
├── index.html            # Aplicación completa (Panel Admin + Vista Cliente + Turnero)
├── MANUAL_USUARIO.md     # Documentación operativa para el barbero
└── MANUAL_TECNICO.md     # Manual de arquitectura, persistencia y API
```

---

## 2. Esquema de Persistencia (LocalStorage)

Los datos locales se estructuran bajo las siguientes claves:

### 1. `barberia_settings`
```typescript
{
  salonName: string;          // "Barbería · Nico"
  salonLogo: string;          // Base64 comprimido o URL de imagen
  salonPhone: string;         // Número de WhatsApp "54911..."
  paymentAlias: string;       // Alias Mercado Pago / CVU
  paymentHolder: string;      // Titular de la cuenta
  template: string;           // Plantilla de mensaje con tags {nombre}, {servicio}, {semanas}
  bookingEnabled: boolean;    // Estado del turnero online
  bookingStartHour: number;   // Hora apertura (ej: 9)
  bookingEndHour: number;     // Hora cierre (ej: 20)
  workDays: number[];         // Días habilitados [1, 2, 3, 4, 5, 6]
  loyaltyEnabled: boolean;    // Programa de sellos activo
  loyaltyTarget: number;      // Cantidad de sellos para recompensa (default: 6)
  loyaltyReward: string;      // "1 Corte Gratis"
}
```

### 2. `barberia_clients`
```typescript
Array<{
  id: string;                 // "c_1730000000000"
  name: string;               // Nombre del cliente
  phone: string;              // Teléfono WhatsApp
  lastCutDate: string;        // "YYYY-MM-DD"
  habitualService: string;    // "Degradé + Barba"
  notes: string;              // Preferencias particulares de corte
  stamps: number;             // Sellos acumulados
  totalVisits: number;        // Contador histórico
  debt: number;               // Deuda pendiente en ARS $ (0 = al día)
}>
```

---

## 3. Motor de Turnero en la Nube & Anti-Colisión

* **Identificador de App:** `CLOUD_APP_ID = 'barberia'`
* **Endpoint Cloud:** API Worker en la nube que gestiona la matriz de horarios por fecha (`YYYY-MM-DD`).
* **Freno de Colisión:**
  1. `fetchCloudDay(dateStr)` consulta el estado del día en tiempo real justo antes de enviar la reserva.
  2. Si `latestDay.closed === true` o `latestDay.hours.includes(hourKey)`, se aborta la transacción y se notifica al usuario con render en gris.
  3. Si está libre, se añade el horario al array `hours`, se persiste en la nube con `saveCloudDay` y se almacena el detalle del cliente en `saveCloudSlotDetail`.
* **Modo Dueño (Agenda Manual):**
  * La dueña o barbero puede ejecutar `toggleOwnerCloudSlot(hourKey)` para bloquear o liberar horarios de forma inmediata.
  * Botón `toggleOwnerCloudDay()` permite cerrar o abrir la jornada completa en la nube.

---

## 4. Generación Robusta de Códigos QR

El sistema de cobro en mostrador implementa tolerancia a fallos de dos niveles:
1. **Motor Primario:** Librería `QRCode.js` ejecutada localmente en el cliente sin requerir salida externa.
2. **Fallback API:** Si la renderización local arroja excepción, la función recurre inmediatamente a la API de `QuickChart.io` (`https://quickchart.io/qr?text=...`) inyectando el elemento `<img>`.
3. **Payload:** Formateado para transferencias directas compatibles con billeteras argentinas:
   `https://mpago.la/transfer?alias={ALIAS}&amount={MONTO}`

---

## 5. Mantenimiento y Buenas Prácticas

1. **Modificaciones de Código:** Realizar cambios quirúrgicos sobre funciones aisladas para no alterar el estado de Tailwind ni los listeners de eventos.
2. **Formato Argentino:** Toda salida monetaria debe utilizar `formatCurrency()` con formato `$ XX.XXX` (ARS) y horarios en GMT-3 (24hs).
