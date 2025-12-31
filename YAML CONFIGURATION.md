### Démarrage progressif ( ramp-up ) :

```yaml
   
alias: AC70 Démarrage progressif
mode: single
trigger:
  - platform: state
    entity_id: switch.ac70_marche
    to: "on"
action:
  - repeat:
      sequence:
        - service: number.set_value
          target:
            entity_id: number.ac70_frequence_consigne
          data:
            value: "{{ repeat.index * 5 }}"
        - delay: "00:00:03"
      until:
        - condition: template
          value_template: "{{ repeat.index * 5 >= 50 }}"
```

### Sécurité température :

```yaml

alias: AC70 Arrêt sécurité température
trigger:
  - platform: numeric_state
    entity_id: sensor.ac70_temperature_variateur
    above: 80
action:
  - service: switch.turn_off
    target:
      entity_id: switch.ac70_marche
```

### Interdiction inversion en marche :

```yaml

alias: AC70 Sécurité sens rotation
trigger:
  - platform: state
    entity_id: switch.ac70_sens_rotation
action:
  - condition: state
    entity_id: switch.ac70_marche
    state: "off"
  - service: homeassistant.turn_on
    target:
      entity_id: switch.ac70_sens_rotation
```


