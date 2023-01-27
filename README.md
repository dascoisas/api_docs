# API Documentation

## Introduction

The API is focused on testing devices requirements and features. (eg. SLC's led on/off status).

## Guide

1. Get the Device MAC IP Address from the 8585 HTTP port. (eg. http://<GATEWAY_IP_ADDRESS>:8585/).
2. Select "All Documentations" and choose the project (eg. EVB, SLC or Gridsafe).
3. Select the version.
4. Paste the address on the search tool and press OK.

Then you'll see all the developed features for the device.

### GET/PUT/DELETE

The API works using HTTP methods. 

#### GET

The **GET** method returns a HTTP request based on the information at the "Example" tab:

- **RESPONSE:** The reply from the device following the Example template.
- **CLEAR:** Clear the reply string.
- **MODEL:** It shows each variable meaning, type and description.
- **EXAMPLE:** Shows an example template for the request.

#### PUT
The **PUT** method send a HTTP request based on the "Example" tab:

- **RESPONSE:** Sucess or Error.
- **CLEAR:** Clear the reply string.
- **MODEL:** It shows each variable meaning, type and description.
- **EXAMPLE:** Shows the string example that you should modify before "TRY".

#### DELETE
The **DELETE** method send a HTTP request that usually deletes a variable value (clear) or reset it (set to zero).

- **RESPONSE:** Sucess or Error.