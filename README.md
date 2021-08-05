# Nokia SIP
This is a script to generate configurations for SIP on older Nokia phones.

Currently supported phones are:
* Nokia 208 Dual-SIM
* Nokia 515 Single-SIM

with more to come soon.

Only Linux is supported right now. Windows support is planned for the future.

## Prerequisets
* `python3`
* `libexpat1-dev` (might only be for building `libwbxml` - needs further testing)

`libwbxml` (https://github.com/libwbxml/libwbxml) is provided in `libwbxml/`.

## Usage
`./confGen {deviceType} {username} {password} {server}`

By default, a `config.prov` file will be generated to be pushed to the phone (note: **this must be done by BlueTooth**). You can specify a different output file by passing `--output`.

### Other options
```
$ ./confGen -h
usage: ./confGen [-h] [--provName PROVNAME] [--port PORT] [--proxy PROXY]
                 [--proxyPort PROXYPORT] [--output OUTPUT]
                 {nokia208dual.xml,nokia515single.xml} username password
                 server

Generate provisioning files for Nokia SIP

positional arguments:
  {nokia208dual.xml,nokia515single.xml}
                        Device type
  username              SIP Username
  password              SIP Password
  server                SIP Server

optional arguments:
  -h, --help            show this help message and exit
  --provName PROVNAME   Name for provisioning profile (default 'Nokia SIP')
  --port PORT           SIP Port (default 5060)
  --proxy PROXY         SIP Proxy
  --proxyPort PROXYPORT
                        SIP Proxy Port (default 5060)
  --output OUTPUT       Output file (default config.prov)
  ```

## Supporting more phones
Create a new file in `templates/`. Use format "`{device}.xml`" for the file name.

You can use the following parameters anywhere in the file, which will be replaced by `confGen`:

| Template Parameter | CLI Parameter |
|--- | --- |
| `{NAME}` |`--provName` |
|`{PORT}` | `--port` |
| `{REGISTRAR}` | `--proxy` |
| `{REGISTRAR_PORT}` | `--proxyPort` |
| `{USER}` | `username` |
| `{PASSWORD}` | `password` |
| `{DOMAIN}` | `server` |

## Planned future features
* STUN
* Custom SIP expiry
* TCP
* Pushing generic configurations and then allowing the user to sign into an account directly on-device