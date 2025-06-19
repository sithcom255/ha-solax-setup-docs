---
title: Welcome to Solax with Home Assistant
tags:
  - documentation
---

## Scope

### What is this for?
Handling of the solax invertor based on day-ahead planning, which allows efficient use of battery and photovoltaics.
Some situations where this can help you:

+ Sell in the morning directly to grid if you know that the battery will anyway get charged.
+ Discharge battery in the evening at maximum price for profit.
+ Buy low and sell high (Almost never happens).
+ Charge at low price to avoid expensive hours from grid.

#### Limitations
+ No support for scheduled loads (EMHASS does support it), should be easy to add.
+ One day ahead planning.
+ Based on yaml entities + pyscript + automations, so at least some understanding is needed.
+ There is no support for this setup. If you do not know what to do use Claude, chatGPT or friend.

### Who is this for?
For people who do not have much experience with programing, but have an ambition to play around with
home assistant. Eg. you already integrate some lights, cameras, AC or want to in future. If you already own home assistant,
the setup usually requires to install the integrations/addons, set it up and then add the knobs for controlling.
There is for each section short and long description of what you need to do.

For experienced programmers, feel free to scroll down to the relevant code sections.

### Where is the guide?

[Go to the guide.](./guide/1_intro.md)

## Contents of the guide

### Overview

![Overview](./assets/architecture_light.svg#only-light)
![Overview](./assets/architecture_dark.svg#only-dark)

### Topics

1. [Preparation](./guide/1_intro.md)
2. [External Connectivity](./guide/2_external_connectivity.md)
3. [Core used components](./guide/3_components.md)
4. [Setup knobs and levers](./guide/4_entities.md)
5. [Pyscript](./guide/5_pyscript.md)
6. [Solax automations](./guide/6_solax_automations.md)
7. [Custom control dashboard](./guide/7_monitoring.md)

### Core components

- Home assistant
- [HACS](https://www.hacs.xyz/)
- [Solax Modbus](https://github.com/wills106/homeassistant-solax-modbus)
- [EMHASS](https://github.com/davidusb-geek/emhass)
- [Pyscript](https://github.com/custom-components/pyscript)
- [Czech Energy Spot Prices](https://github.com/rnovacek/homeassistant_cz_energy_spot_prices)
- [Weather Forecast](https://github.com/rany2/ha-open-meteo-solar-forecast)
- [Advanced Terminal](https://github.com/hassio-addons/addon-ssh/)

### Other addons in my setup:
- [Nginx](https://github.com/hassio-addons/addon-nginx-proxy-manager)
- [Cloudflared](https://github.com/brenner-tobias/addon-cloudflared)
- [InfluxDb](https://www.home-assistant.io/integrations/influxdb)
- [Grafana](https://github.com/hassio-addons/addon-grafana)



