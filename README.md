# homeassistant-difusor-bano

# 💨 Automatización inteligente para difusor de baño (Home Assistant)

Este proyecto incluye:

- 🕑 Automatización que enciende un humidificador cada 2 horas entre las 06:00 y las 21:00.
- 🔘 Lógica que apaga automáticamente el humidificador 5 minutos después de activarlo manualmente (botón físico, app, etc.).
- 💡 Scripts que controlan tanto el humidificador como la bombilla incorporada.

---

## 🛠️ Instrucciones

### 1. Crear los dos scripts
- Añade los scripts a través del editor de scripts o en `scripts.yaml`.

### 2. Crear las dos automatizaciones
- Ve a **Automatizaciones → Crear**
- Edita en modo yaml y pega el código de ambas automatizaciones.
- (`Difusor aromas baño`) y (`Difusor baño - apagado automático tras encendido manual`)
- Selecciona:
  - El humidificador (`humidifier.humidificador_bano`)
  - Script de encendido (`script.humidificador_bano_on`)
  - Script de apagado (`script.humidificador_bano_off`)

### 3. ¡Listo!
Tu baño quedará automatizado para que el difusor:
- Se active automáticamente cada 2 horas.
- Se apague tras 5 minutos.
- También se apague automáticamente si tú lo activas manualmente.

---

## 🧪 Requisitos

- Home Assistant 2023.3 o superior recomendado.
- Entidad tipo `humidifier` con control de encendido/apagado.
- Luz opcional conectada al mismo dispositivo.

---

## ⚙️ script.humidificador_bano_on.yaml
```
alias: Humidificador baño on
sequence:
  - service: humidifier.turn_on
    target:
      entity_id: humidifier.humidificador_bano
  - service: light.turn_on
    target:
      entity_id: light.humidificador_bano_lightbulb
```

## ⚙️ script.humidificador_bano_off.yaml
```
alias: Humidificador baño off
sequence:
  - service: humidifier.turn_off
    target:
      entity_id: humidifier.humidificador_bano
  - service: light.turn_off
    target:
      entity_id: light.humidificador_bano_lightbulb
```

## 🧭 Automatización 1
```
alias: Difusor aromas baño
description: ""
triggers:
  - hours: /2
    minutes: 0
    seconds: 0
    trigger: time_pattern

conditions:
  - condition: and
    conditions:
      - condition: time
        after: "06:00:00"
        before: "21:01:01"
      - condition: time
        weekday:
          - mon
          - tue
          - wed
          - thu
          - fri
          - sat
          - sun

actions:
  - target:
      entity_id: script.humidificador_bano_on
    action: script.turn_on
    data: {}
  - delay:
      hours: 0
      minutes: 5
      seconds: 0
      milliseconds: 0
  - target:
      entity_id: script.humidificador_bano_off
    action: script.turn_on
    data: {}

mode: queued
max: 3
```

## 🖲️ Automatización 2

```
alias: Difusor baño - apagado automático tras encendido manual
description: "Apaga el humidificador 5 minutos después de cualquier encendido"
triggers:
  - platform: state
    entity_id: humidifier.humidificador_bano
    to: "on"

actions:
  - delay:
      minutes: 5
  - target:
      entity_id: script.humidificador_bano_off
    action: script.turn_on
    data: {}

mode: restart
```
