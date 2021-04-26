Required HA Integration

* [Node-RED Companion Integration](https://github.com/zachowj/hass-node-red)

Required Node-Red nodes

* [node-red-contrib-tesla](https://github.com/onokje/node-red-contrib-tesla)
* [node-red-contrib-home-assistant-websocket](https://github.com/zachowj/node-red-contrib-home-assistant-websocket)

Create Helpers

* input_boolean.tesla_honk
* input_boolean.tesla_locks
* input_boolean.tesla_climate
* input_boolean.tesla_vent

Flow

* Import [node-red flow](https://github.com/jgthornburgh/homeassistant-config/blob/master/tesla-flow.json)
  ![text](https://github.com/jgthornburgh/homeassistant-config/blob/master/flow%20pics/get_data.PNG)
  ![text](https://github.com/jgthornburgh/homeassistant-config/blob/master/flow%20pics/send_command.PNG)
  
Create Switch template for climate

    switch:
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

Create Lock  template for door locks

    lock:
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
            entity_id: input_boolean.tesla_locks
            

