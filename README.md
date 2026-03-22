# ESPHome Templates
Modular, reusable components to pull into various ESPHome projects so I'm not writing the same damn code every time.

### The problem
Often when buying an ESP dev board, they're in bundles of 3+, so I'll "force" myself to use that type of board for multiple different projects.
ESPHome has a lot of (important) boilerplate-like code that each of the projects can share, from the ESPHome config, the ESP board config, and even many of the sensors I use across various projects.

This repo allows me to pick and choose the board or sensor(s) and get a lot of the boilerplate code stuffs out of the way.

### The solution (example)
Cheap-Yellow-Displays (CYDs) are common resistive touchscreen devices that are, as the name implies, cheap. If you're buying one, why not buy 5?


#### Before ESPHome Templates
```
substitutions:
  #CYD common pin labels
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

esp32:
  variant: esp32
  framework:
    type: esp-idf

i2c:
  - sda: ${i2c_sda}
    scl: ${i2c_scl}
    scan: true

spi:
  - id: tft
    clk_pin: ${tft_clk}
    mosi_pin: ${tft_mosi}
    miso_pin:
      number: ${tft_miso}
      ignore_strapping_warning: true
  - id: touch
    clk_pin: ${touch_clk}
    mosi_pin: ${touch_mosi}
    miso_pin: ${touch_miso}

# Screen
display:
  - id: main_display
    platform: ili9xxx
    model: ili9342
    rotation: ${rotation}
    spi_id: tft
    cs_pin: ${tft_cs}
    dc_pin: ${tft_dc}
    color_order: BGR
    invert_colors: False
    update_interval: never
    auto_clear_enabled: false

touchscreen:
  - id: main_touchscreen
    platform: xpt2046
    spi_id: touch
    cs_pin: ${touch_cs}
    interrupt_pin: ${touch_interupt}
    threshold: 400
    calibration:
      x_min: 280
      x_max: 3860
      y_min: 340
      y_max: 3860
    transform:
      mirror_x: true
```


#### After ESPHome Templates
```
substitutions:
  device_name: mycool_cyd
  friendly_name: My Cool CYD Project
  rotation: 90

  packages:
    esphome_templates:
      url: https://github.com/TemuWolverine/esphome_templates
      ref: main
      files:
        - esphome_boilerplate.yaml
        - boards/cyd_with_default_pins
```

Then the CYD app code can be added.
