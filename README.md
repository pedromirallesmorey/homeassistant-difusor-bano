# homeassistant-difusor-bano
💨 Automatización inteligente para difusor de baño (Home Assistant)

## 🚀 Importar directamente

Si quieres usar esta automatización como blueprint desde GitHub:

[![Importar Blueprint en Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/pedromirallesmorey/difusor-bano&file_path=blueprints/automation/tu_usuario/difusor_bano_automatico.yaml)

---

## 🛠️ Instrucciones

### 1. Subida manual
- Copia el blueprint a:  
  `/config/blueprints/automation/tu_usuario/difusor_bano_automatico.yaml`
- Añade los scripts a través del editor de scripts o en `scripts.yaml`.

### 2. Crear la automatización
- Ve a **Automatizaciones → Crear → Usar Blueprint**
- Elige el blueprint: `Difusor baño automático + apagado tras encendido manual`
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
