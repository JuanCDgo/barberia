# 💈 Manual de Usuario · Barbería

¡Bienvenido al sistema integral de gestión de clientes, agenda en la nube y cobro para tu barbería! Esta aplicación web está optimizada para celulares y computadoras, pensada para que atiendas rápido en el sillón, envíes recordatorios por WhatsApp en 1 toque, cobres con QR y permitas a tus clientes reservar turnos online sin superposiciones.

---

## 1. Pantalla Principal: ¿Qué vas a ver?

1. **Encabezado:**
   * **Nombre y Logo:** Podés personalizar tu logo y el nombre de la barbería tocando el avatar o la ruedita de ajustes.
   * **Badge de Turnero:** Muestra si el turnero online está activo (`🟢 Turnero Activo`) o pausado.
   * **📷 Cobro QR:** Acceso rápido para mostrar en pantalla tu QR de Mercado Pago o transferencias.
   * **⚙️ Ajustes:** Configuración del local, horarios, WhatsApp y copia de seguridad en Google Drive.

2. **Panel de Clientes:**
   * Lista de clientes con fecha del último corte, servicio habitual y estado.
   * **Sin etiquetas redundantes:** Si el cliente está al día no molesta; si tiene saldo pendiente aparece destacado en rojo con botón directo a cobro QR.
   * **Filtros rápidos:** Ver todos, los que necesitan corte (recordatorios) o los que tienen deuda.

3. **Acciones Rápidas en cada Tarjeta:**
   * **💬 WhatsApp:** Envía el mensaje de recordatorio automático formateado en 1 toque.
   * **⭐ Sumar Sello:** Acredita una visita en la tarjeta de fidelidad del cliente con lluvia de confeti.
   * **💳 Cobrar:** Abre el modal de cobro QR con el monto exacto adeudado en pesos argentinos (ARS $).

---

## 2. Flujo de Trabajo Diario

### Registrar o Atender a un Cliente
1. Tocá el botón verde flotante **+ Nuevo Cliente**.
2. Ingresá el **Nombre** y su número de **WhatsApp** (con código de área sin el 15).
3. Seleccioná el servicio habitual (ej: *Corte Clásico*, *Corte + Barba*, *Degradé*).
4. Guardá los datos. Si es un cliente nuevo, se crea su ficha automáticamente.

### Enviar Recordatorio de Corte por WhatsApp
1. En la lista vas a ver cuántas semanas pasaron desde la última visita (ej: `Hace 3 semanas`).
2. Tocá el botón de **WhatsApp**.
3. Se abrirá la conversación con un mensaje personalizado:
   > *"¡Hola Juan! Ya pasaron 3 semanas de tu Degradé + Barba, ¿te reservo turno en la barbería?"*
4. Enviás el mensaje en 1 toque sin tener que tipear nada.

---

## 3. Turnero Online en la Nube con Bloqueo Real

Tus clientes pueden reservar sus propios turnos desde su celular:
1. En **Ajustes**, activá el switch **Turnero Online**.
2. Copiá el enlace público del turnero o tocalo para probarlo.
3. **Bloqueo Real:** Cuando un cliente reserva un horario (ej: 18:00 hs), el turno se bloquea en la nube en tiempo real. Para todos los demás celulares aparecerá inmediatamente en gris claro (`🔒 Ocupado`).
4. **Freno de Colisión:** Si dos personas intentan reservar el mismo horario al mismo segundo, el sistema bloquea al segundo y le pide elegir otro horario disponible.
5. **📅 Control Manual del Barbero (Agenda):**
   * Desde el panel podés abrir **📅 Control Manual de Horarios**.
   * Podés ocupar manualmente un turno (si alguien te llamó por teléfono o cayó al local).
   * Podés liberar un horario cancelado.
   * Podés cerrar un día completo (feriado, franco o descanso) con 1 solo toque.

---

## 4. Cobro con QR (Mercado Pago y Transferencias)

* Tocá el botón **📷 Cobro QR** en el encabezado o en la ficha de un cliente que deba dinero.
* Se genera en pantalla el código QR dinámico vinculado a tu Alias/CBU y el monto en pesos argentinos ($ ARS).
* El cliente escanea con Mercado Pago, MODO o cualquier app bancaria y te abona en el acto.
* **Fallback anti-cortes:** Si por algún motivo se cae una conexión, la app cambia automáticamente a un motor alternativo de QR para que nunca te quedes sin cobrar.

---

## 5. Respaldo y Copia de Seguridad

* **Google Drive Automático:** Al configurar tu webhook de Drive, la app sincroniza una copia de seguridad periódicamente sin que tengas que hacer nada.
* **Exportar / Importar JSON:** Desde los ajustes podés descargar un archivo `.json` a tu computadora o celular para guardarlo en un pendrive o restaurarlo en otro dispositivo.
