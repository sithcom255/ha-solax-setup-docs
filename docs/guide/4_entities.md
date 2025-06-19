---
title: Setup knobs and levers
tags:
  - documentation
---

#### Configuration.yaml entities

Let's start by adding the helper entities which we use for controlling the setup. Notice the comments.

```yaml
# our entities for invertor overview
input_select:
  # managed by the python script, will get overriden if the input_boolean.automatic_invertor_control_enabled is true
  # if you turn the automatic_invertor_control_enabled to false, we
  invertor_strategy:
    name: Invertor Strategy
    options:
      - Sell to grid
      - Charge
      - Discharge
      - No action
    initial: No action
    icon: mdi:strategy

input_boolean:
  # managed by the python script
  export_allowed:
    name: Export allowed
    icon: mdi:home-export-outline
  # this is for you to touch
  automatic_invertor_control_enabled:
    name: Automatic Invertor Control Enabled
    icon: mdi:brain

input_number:
  # this value will define the value which the export_limit is restored
  # you can override this
  maximum_export_allowed:
    name: Maximum export when export allowed
    initial: 11600
    min: 0
    max: 11600
    step: 100
    mode: box
  # what is the price at which we will start selling, set as you wish
  export_price_threshold:
    name: Sell threshold
    initial: 0
    min: 0
    max: 10
    mode: box
```

