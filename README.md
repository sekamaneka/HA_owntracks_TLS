# HA_owntracks_TLS


Edit generate_CA and include `<hostname>` of your mqtt server in HOSTLIST.
./generate_CA `<hostname>`
./generate_CA client `<client_name>`

openssl pkcs12 \
  -export \
  -in jjolie.crt \
  -inkey jjolie.key \
  -name "Jane's certificate/key" \
  -out jjolie.p12
