# Power Flow Card Plus Custom — v1.0.0

A standalone Home Assistant Lovelace card for live power and historical energy.

## Included

- Power mode: live W / kW.
- Energy mode: cumulative Wh / kWh sensors calculated from Home Assistant history.
- Periods: Today, Yesterday, Week, Month, custom From–To.
- Per-entity Deadband / zero tolerance.
- Per-entity rounding and live smoothing (Solar and Individual GUI expose all; Grid/Battery expose deadband in v1.0 UI and accept the same object options in YAML).
- Grid import/export, Solar, Battery charge/discharge/SOC, calculated Home, unlimited Individual devices.
- Graphical card editor with Home Assistant sensor picker.
- English, Russian, Hebrew and RTL for Hebrew.
- Click entities for More Info.
- Can be installed alongside the original Power Flow Card Plus.

## Install with HACS

Add this repository as a HACS **Custom repository**, category **Dashboard**, then install **Power Flow Card Plus Custom**. The distributed file is `power-flow-card-plus-custom.js`.

Card type: `custom:power-flow-card-plus-custom`.

### Example

```yaml
type: custom:power-flow-card-plus-custom
mode: power
language: ru
title: Power Flow
entities:
  grid:
    consumption:
      entity: sensor.import_power
      deadband: 200
    production:
      entity: sensor.export_power
      deadband: 200
  solar:
    entity: sensor.total_dc_power
    deadband: 100
    rounding: 10
    smoothing: 5
  battery:
    consumption:
      entity: sensor.battery_discharging_power
      deadband: 100
    production:
      entity: sensor.battery_charging_power
      deadband: 100
    state_of_charge: sensor.battery_level
  individual:
    - entity: sensor.car_charger_power
      name: Car
      deadband: 100
```

For Energy mode choose cumulative energy sensors and set `mode: energy`. The card reads the selected Home Assistant history interval and accumulates positive counter changes; a counter reset is handled by continuing from the new post-reset value.

## License / attribution

MIT. Inspired by Power Flow Card Plus / flixlix. The upstream MIT license and attribution are preserved in this repository.
