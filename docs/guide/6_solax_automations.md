---
title: Solax Automations
tags:
  - documentation
---


#### Logic

We have a strategy selector updating our helper entity. These automations are realizing the strategy towards the
solax. Remember the Self Use Mode that we are using as setup in the components? That will be our No action strategy.
There are however few cases there we want to hande the invertor with remote control.
If you want to truly understand, please read [docs](https://homeassistant-solax-modbus.readthedocs.io/en/latest/modbus-power-control/).

Handled situations:

- Charging
- Discharge
- Sell to grid

#### Configuration.yaml

Uncomment this section.

```yaml
automation: !include_dir_list automations
script: !include scripts.yaml
scene: !include scenes.yaml

```

#### Automations

Create a folder with the automations is /config/automations

=== "`charge.yaml`add"
    ``` yaml
    alias: Charge the batter either from the grid or pv - 10m
    description: "Charge"
    triggers:
      - trigger: time_pattern
        minutes: "/10"
      - trigger: state
        entity_id: input_boolean.automatic_invertor_control_enabled
      - trigger: state
        entity_id: input_select.invertor_strategy

    condition:
      - condition: state
        entity_id: input_boolean.automatic_invertor_control_enabled
        state: "on"
      - condition: state
        entity_id: input_select.invertor_strategy
        state: "Charge"

    # Charge from the grid, by enabling the battery to only import, this means that all will go from the grid
    # not sure about some negative scenarios

    action:
      - service: select.select_option
        data:
          option: Enabled Battery Control
        target:
          entity_id:
            - select.solax_remotecontrol_power_control
      - service: number.set_value
        data:
          value: "{{ (states('sensor.p_batt_forecast') | float / 100) | round(0) * 100 }}"
        target:
          entity_id: number.solax_remotecontrol_active_power
      - service: number.set_value
        data:
          value: "606"
        target:
          entity_id: number.solax_remotecontrol_autorepeat_duration
      - service: number.set_value
        data:
          value: 12000
        target:
          entity_id: number.solax_remotecontrol_import_limit
      - service: button.press
        data: {}
        target:
          entity_id: button.solax_remotecontrol_trigger
    mode: single
    ```
=== "`discharge.yaml`"
    ``` yaml
    alias: Discharge the battery to the grid or to the house load
    description: ""
    triggers:
      - trigger: time_pattern
        minutes: "/10"
      - trigger: state
        entity_id: input_boolean.automatic_invertor_control_enabled
      - trigger: state
        entity_id: input_select.invertor_strategy
    condition:
      - condition: state
        entity_id: input_boolean.automatic_invertor_control_enabled
        state: "on"
      - condition: state
        entity_id: input_select.invertor_strategy
        state: "Discharge"

    # Discharge the battery, this is reasonably

    action:
      - service: select.select_option
        data:
          option: Enabled Battery Control
        target:
          entity_id:
            - select.solax_remotecontrol_power_control
      - service: number.set_value
        data:
          value: "{{ -( (states('sensor.p_batt_forecast') | float / 100) | round(0) * 100) }}"
        target:
          entity_id: number.solax_remotecontrol_active_power
      - service: number.set_value
        data:
          value: "606"
        target:
          entity_id: number.solax_remotecontrol_autorepeat_duration
      - service: number.set_value
        data:
          value: 12000
        target:
          entity_id: number.solax_remotecontrol_import_limit
      - service: button.press
        data: {}
        target:
          entity_id: button.solax_remotecontrol_trigger
    mode: single
    ```

=== "`sell_no_store.yaml`"
    ``` yaml
    alias: Sell no store - 10m
    description: ""
    triggers:
      - trigger: time_pattern
        minutes: "/10"
      - trigger: state
        entity_id: input_boolean.automatic_invertor_control_enabled
      - trigger: state
        entity_id: input_select.invertor_strategy

    condition:
      - condition: state
        entity_id: input_boolean.automatic_invertor_control_enabled
        state: "on"
      - condition: state
        entity_id: input_select.invertor_strategy
        state: "Sell to grid"
    #
    # this is the only way to force the safe selling, this forces the battery to not charge.
    # but you can still push energy in and out (in case of some fuckup).
    # low load cases
    #
    # with E_BATTERY_CONTROL
    # positive -> charge
    # negative -> discharge
    # 0 no battery
    #
    action:
      - service: select.select_option
        data:
          option: Enabled Battery Control
        target:
          entity_id:
            - select.solax_remotecontrol_power_control
      - service: number.set_value
        data:
          value: "0"
        target:
          entity_id: number.solax_remotecontrol_active_power
      - service: number.set_value
        data:
          value: "606"
        target:
          entity_id: number.solax_remotecontrol_autorepeat_duration
      - service: number.set_value
        data:
          value: 12000
        target:
          entity_id: number.solax_remotecontrol_import_limit
      - service: button.press
        data: {}
        target:
          entity_id: button.solax_remotecontrol_trigger
    mode: single
    ```
=== "`publish.yaml`"
    ```yaml
          alias: "Ensure that that emhass data gets published each 5 minutes."
        triggers:
          - trigger: time_pattern
            minutes: "/5"
        action:
          - service: shell_command.publish_data
    ```

Please setup these automations and you are quite good to go!!!


