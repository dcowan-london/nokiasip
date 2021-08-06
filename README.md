# Nokia SIP
This is a script to generate configurations for SIP on older Nokia phones.

Currently supported phones are:
* Nokia 208 Dual-SIM
* Nokia 515 Single-SIM

with more to come soon.

Only Linux is supported right now. Windows support is planned for the future.

## License
### NOKIA SIP PROV GENERATOR
NOKIA SIP PROV GENERATOR
Copyright (C) 2021  Dovi Cowan
nokiasip@catch.dovicowan.email

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

### libwbxml
libwbxml, the WBXML Library.
Copyright (C) 2002-2008 Aymerick Jehanne <aymerick@jehanne.org>
Copyright (C) 2011 Michael Bell <michael.bell@opensync.org>

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA

LGPL v2.1: http://www.gnu.org/copyleft/lesser.txt

Contact: aymerick@jehanne.org
Home: http://libwbxml.aymerick.com

## Prerequisites
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