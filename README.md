# HA_owntracks_TLS
### Depending on your configuration you may have to prepend sudo to all following commands.
1. Download a set of tools provided by Owntracks to setup the mqtt broker mosquitto along with TLS. 
 * `git clone https://github.com/owntracks/tools.git`
2. Change to the downloaded directory.
 *  `cd tools/`
3. Execute the setup script.
 *  `sudo chmod +x mosquitto-setup.sh`
 *  `sudo ./mosquitto-setup.sh`
4. This will install a basic mosquitto configuration directory in /etc/mosquitto.
5. The actual configuration file is in /etc/mosquitto/conf.d/mosquitto.conf. We will edit this later.

1. Copy the generate_CA script to the mosquitto config folder and edit it to include the `<hostname>` of your mqtt broker's server in `HOSTLIST=` in line 42. If you are using a Raspberry Pi the `<hostname>` will probably be raspberrypi. In any case it can be found by running this command `cat /etc/hosts`.
 * `mkdir /etc/mosquitto/certs`
 * `cp -a ./owntracks/tools/TLS/generate_CA /etc/mosquitto/certs/`
 * `cd /etc/mosquitto/certs/`
 * `gedit generate_CA`
2.  Now we are ready to start generating our certificates. The following command will generate 6 files. All files starting with ca will be your certificate authority that will be used to sign everything else and the files starting with `<hostname>` will be your server certificates.
  * `./generate_CA <hostname>`
    * `ca.crt`
    * `ca.srl`
    * `ca.key`
    * `<hostname>.crt`
    * `<hostname>.csr`
    * `<hostname>.key`
3.  The following command will generate your `<client>` certificates. You can generate multiple, one for each client that will be connecting to your broker. They will be used to provide authentication. If you decide to skip this step the communication will be encrypted but not authenticated.
  * `./generate_CA client <client_name>`
    * `<client_name>.crt`
    * `<client_name>.csr`
    * `<client_name>.key`

`openssl pkcs12
  -export
  -in <client_name>.crt
  -inkey <client_name>.key
  -name "Client's certificate/key"
  -out <client_name>.p12`
