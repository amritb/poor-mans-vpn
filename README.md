# Poor man's VPN

An ansible playbook to set up wireguard server.


## Setup
- Create a vm at your desired location from your desired provider
- Make sure you can ssh into the machine with default public key
- Install & start the wireguard client app
- Create an empty tunnel
- Copy the client private key

```
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
deactivate
```
## Run the playbook
```
source venv/bin/activate
ansible-playbook -i <server public ip>, -u <server username> playbook.yaml
```
#### Prompts
```
Client public key: <copy from wireguard client app>
Allowed IPs [10.0.0.3]: 
Wireguard listen port [51820]: 
```
> Running the playbook multiple times will change the server private/public keys. 
> Make sure to copy the new public key into the client config each time.

## Client config
```
[Interface]
PrivateKey = <auto generated for client>
Address = 10.0.0.3/24
DNS = 1.1.1.1, 1.0.0.1

[Peer]
PublicKey = <server wg public key / changes every time we run the playbook>
AllowedIPs = 0.0.0.0/0
Endpoint = <server public ip>:<wg port>
```