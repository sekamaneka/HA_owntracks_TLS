# HA_owntracks_TLS


1.  Edit generate_CA and include `<hostname>` of your mqtt server in HOSTLIST.
2.  `./generate_CA <hostname>`
3.  `./generate_CA client <client_name>`

`openssl pkcs12
  -export
  -in <client_name>.crt
  -inkey <client_name>.key
  -name "Client's certificate/key"
  -out <client_name>.p12`
