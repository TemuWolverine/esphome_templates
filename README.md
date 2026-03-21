# ESPHome Templates
Modular, reusable components to pull into various ESPHome projects  so I'm not writing the same damn code every time

### Example usage

```
substitutions:
  device_name: waterytart_cyd
  friendly_name: WateryTart_CYD
  min_version: 2025.11.0
  rotation: 90

  i2c_sda: "27"
  i2c_scl: "22"

  tft_clk: "14"
  tft_mosi: "13"
  tft_miso: "12"
  tft_cs: "15"
  tft_dc: "2"

  touch_clk: "25"
  touch_mosi: "32"
  touch_miso: "39"
  touch_cs: "33"
  touch_interupt: "36"

  packages:
    esphome_templates:
      url: https://github.com/TemuWolverine/esphome_templates
      ref: main
      files:
        - esphome-boilerplate.yaml
        - boards/cyd.yaml
```

Then the CYD app code can be added.
