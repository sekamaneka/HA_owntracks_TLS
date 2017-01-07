# HA_owntracks_TLS
1. Download a set of tools provided by Owntracks to setup the mqtt broker along with TLS. 
 * `git clone https://github.com/owntracks/tools.git`

### Depending on your configuration you may have to prepend sudo to all following commands.
1. Copy the generate_CA script from /owntracks/toosl/TLS/ to /etc/mosquitto/certs/ and edit it with `gedit generate_CA` and include the `<hostname>` of your mqtt broker's server in `HOSTLIST=` in line 42.
 * `mkdir /etc/mosquitto/certs
 * `cp -a ./owntracks/tools/TLS/generate_CA /etc/mosquitto/certs/`
 * `cd /etc/mosquitto/certs/
 * `gedit generate_CA`
2.  `./generate_CA <hostname>`
  * `ca.crt`
  * `ca.srl`
  * `ca.key`
  * `<hostname>.crt`
  * `<hostname>.csr`
  * `<hostname>.key`
3.  `./generate_CA client <client_name>`
  * `<client_name>.crt`
  * `<client_name>.csr`
  * `<client_name>.key`

`openssl pkcs12
  -export
  -in <client_name>.crt
  -inkey <client_name>.key
  -name "Client's certificate/key"
  -out <client_name>.p12`
