* Use [node-red-contrib-tesla](https://github.com/onokje/node-red-contrib-tesla)
* Import [node-red flow](https://github.com/jgthornburgh/homeassistant-config/blob/master/tesla-flow.json)
  ![text](https://github.com/jgthornburgh/homeassistant-config/blob/master/flow%20pics/get_data.PNG)
  ![text](https://github.com/jgthornburgh/homeassistant-config/blob/master/flow%20pics/send_command.PNG)
* Switch:
    - platform: template
    switches:
      tesla_climate:
        value_template: "{{ is_state('binary_sensor.tesla_climate_on', 'on') }}"
        turn_on:
          service: input_boolean.turn_on
          target:
            entity_id: input_boolean.tesla_climate
        turn_off:
          service: input_boolean.turn_off
          target:
            entity_id: input_boolean.tesla_climate
            
*  lock:
    - platform: template
      name: tesla
      value_template: "{{ is_state('binary_sensor.tesla_locked', 'off') }}"
      lock:
        service: input_boolean.turn_off
        target:
          entity_id: input_boolean.tesla_locks
      unlock:
        service: input_boolean.turn_on
        target:
          entity_id: input_boolean.tesla_locks *
