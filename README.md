# API Documentation

## Introduction

The API is focused on testing devices requirements and features. (eg. SLC's led on/off status).

## YML Structure Example

### File Description

First of all it's necessary describe the *OpenAPI* version and the document description.

- openapi: 3.0.1
- info:
  - version: 6.0.0
  - title: Nouvenn Smart Lighting Controller
  - description: 'This documentation describes the high level REST interface...'

### Tags

The tags are used to split the device's features in segments.

- name: lamp
    - description: Access to lamp parameters

### Paths

Paths are where on the API is the request going for, so you might add some information like this at each path.
```
/lamp/control :
    put:
      tags:
      - lamp
      summary: Update the state of the lamp parameters
      operationId: updateLamp
      requestBody:
        description: ""
        content:
          application/json:
           schema:
             $ref: '#/components/schemas/lamp_control'
        required: true
      responses:
        205:
          description: Success
          content: {}
        400:
          description: Invalid parameters
          content: {}
      x-codegen-request-body-name: body 
    get:
      tags:
      - lamp
      summary: Get the state of the lamp parameters
      description: ""
      operationId: getLamp
      parameters:
      - name: observe
        in: query
        description: "Observe the resource \n\n
                      (none: keep last mode; true: start observing; false: stop observing)"
        required: false
        schema:
          type: boolean
          default: false
      responses:
        200:
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/lamp_control'
```

### Components

This fields describe every variable and field on the GET/PUT/DELETE requests.

- Schemas: The name of the Schema called at the "Paths" field.

```
components:
  schemas:
    lamp_control:
      type: object
      properties:
        state:
          type: integer
          format: int8
          minimum: 0
          maximum: 1
          description: Lamp state (0 for off)
        dim:
          type: integer
          format: int8
          minimum: 0
          maximum: 100
          description: Dimmer value in percentage
        day_night_thr:
          type: integer
          format: int32
          minimum: 0
          maximum: 8386560
          description: "Brightness value in centilux below which the 
                        lamp is switched on, when in 'AUTO LUX' mode. fix \n\n
                        (day_night_thr <= night_day_thr)"
        night_day_thr:
          type: integer
          format: int32
          minimum: 0
          maximum: 8386560
          description: "Brightness value in centilux above which the 
                        lamp is switched off, when in 'AUTO LUX' mode. \n\n
                        (night_day_thr >= day_night_thr)"
        mode:
          type: integer
          format: int8
          minimum: 0
          maximum: 3
          description: "Lamp operation mode:\n\n  
                        0 - MANUAL: Only user commands\n\n
                        1 - AUTO LUX: On/off decision from the luximeter measure\n\n
                        2 - AUTO ASTRO: On/off decision from the solar position\n\n
                        3 - SCHEDULER: On/off decision and dimmer change from scheduled actions"
        dim_mode:
          type: integer
          format: int8
          minimum: 0
          maximum: 1
          description: "Dimmer operation mode:\n\n  
                        0 - Dimmer value output DC between 0 at 10 volts\n\n
                        1 - Dimmer value output DC between 1 at 10 volts"
```

## Usage

1. Get the Device MAC IP Address from the 8585 HTTP port. (eg. http://<GATEWAY_IP_ADDRESS>:8585/).
2. Select "All Documentations" and choose the project (eg. EVB, SLC or Gridsafe).
3. Select the version.
4. Paste the address on the search tool and press OK.

Then you'll see all the developed features for the device.

### GET/PUT/DELETE

The API works using HTTP methods. 

#### GET

The **GET** method returns a HTTP request based on the information at the "Example" tab:

![GET method](/Images/getAPI.png)

- **RESPONSE:** The reply from the device following the Example template.
- **CLEAR:** Clear the reply string.
- **MODEL:** It shows each variable meaning, type and description:

    ![Model Template](/Images/modelAPI.png)

- **EXAMPLE:** Shows an example template for the request.

#### PUT
The **PUT** method send a HTTP request based on the "Example" tab:

![PUT method](/Images/putAPI.png)

- **RESPONSE:** Sucess or Error.
- **CLEAR:** Clear the reply string.
- **MODEL:** It shows each variable meaning, type and description.
- **EXAMPLE:** Shows the string example that you should modify before "TRY".

#### DELETE
The **DELETE** method send a HTTP request that usually deletes a variable value (clear) or reset it (set to zero).

![DELETE method](/Images/deleteAPI.png)

- **RESPONSE:** Sucess or Error.