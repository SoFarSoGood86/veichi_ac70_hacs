
![ODE](https://github.com/user-attachments/assets/9ad2b996-48b0-4c58-bf4c-46b03a38ed77)

# ODE mk3 ArtNet Integration

Intégration Home Assistant pour contrôler le **ODE mk3** via ArtNet.

## Fonctionnalités

* Contrôle des canaux DMX (0–255) via ArtNet.
* Support d’un univers ArtNet vers deux univers DMX.
* Chaque canal DMX exposé comme une entité `light`.
* Retour d’état en temps réel (connectivité, activité, valeurs des canaux).
* Compatible configuration YAML et configuration via l’UI Home Assistant.

## Installation HACS

1. Ajouter le dépôt suivant dans HACS : `https://github.com/SoFarSoGood86/hacs-ode-mk3`
2. Installer l'intégration.
3. Redémarrer Home Assistant.

## Configuration via YAML

```yaml
ode_mk3:
  host: "192.168.1.50"
  port: 6454
  universe: 0
```

## Configuration via UI

1. Aller dans **Paramètres > Intégrations > Ajouter une intégration**.
2. Rechercher `ODE mk3 ArtNet`.
3. Saisir l'IP, le port et l'univers.

## Utilisation

* Chaque canal DMX est disponible comme entité `light` dans Home Assistant.
* Vous pouvez régler l’intensité (0–255) via l’UI ou des automatisations.
* Services disponibles :

  * `ode_mk3.reset_dmx` : Remet tous les canaux à 0.
  * `ode_mk3.refresh_status` : Force la mise à jour des valeurs DMX.

## Exemples d’automatisations

```yaml
- alias: Allumer canal 1
  trigger:
    platform: state
    entity_id: light.ode_mk3_channel_1
    to: 'on'
  action:
    service: light.turn_on
    target:
      entity_id: light.ode_mk3_channel_1
    data:
      brightness: 200
```

## Dépendances

* [python-artnet](https://pypi.org/project/python-artnet/) >=1.0.4

## Code source

[GitHub - SoFarSoGood86/hacs-ode-mk3](https://github.com/SoFarSoGood86/hacs-ode-mk3)
