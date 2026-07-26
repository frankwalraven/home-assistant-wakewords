# home-assistant-wakewords

Deze repository bevat mijn eigen microWakeWord-modellen voor Home Assistant Voice PE.

## Wakewords

- Hey Casa

## Repository

- hey_casa.tflite
- hey_casa.json

---

# Firmware-aanpassingen

Voor gebruik met Home Assistant Voice PE zijn de volgende wijzigingen nodig in `home-assistant-voice.yaml`.

## 1. Wakeword toevoegen

Voeg toe aan het `models:`-blok:

```yaml
- model: https://raw.githubusercontent.com/frankwalraven/home-assistant-wakewords/main/hey_casa.json
  id: hey_casa
```

---

## 2. Gevoeligheid

Gebruik onderstaande instellingen:

```cpp
lambda: |-
  if (x == "Slightly sensitive") {
    id(hey_mycroft).set_probability_cutoff(253);
    id(hey_casa).set_probability_cutoff(204);   // 0.80
  } else if (x == "Moderately sensitive") {
    id(hey_mycroft).set_probability_cutoff(242);
    id(hey_casa).set_probability_cutoff(166);   // 0.65
  } else if (x == "Very sensitive") {
    id(hey_mycroft).set_probability_cutoff(237);
    id(hey_casa).set_probability_cutoff(128);   // 0.50
  }
```

---

## Updateprocedure

Bij een nieuwe release van `esphome/home-assistant-voice-pe`:

1. Sync mijn fork met de officiële repository.
2. Controleer of `home-assistant-voice.yaml` gewijzigd is.
3. Controleer of het `hey_casa`-model nog aanwezig is.
4. Controleer of de bovenstaande `lambda`-instellingen nog aanwezig zijn.
5. Compileer en flash de firmware.
