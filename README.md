# HA_owntracks_TLS


1.  Download this [script](https://github.com/owntracks/tools/blob/master/TLS/generate-CA.sh) provided by Owntracks, edit it with `gedit generate_CA` and include the `<hostname>` of your mqtt broker's server in `HOSTLIST=` in line 42.
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
