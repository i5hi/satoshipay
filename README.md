# satoshipay

The goal of `satoshipay` is to provide a plug and play bitcoin infrastructure management platform for individuals/merchants to manage bitcoin accounts for their physical or online businesses.

## goals

Users:
- freedom maximizing

Admins: 
- secure, light-weight & extendable

Community:
- public sound money infrastructure

## specifications

- bitcoin-only
- all satoshi units
- linux/mac/windows

## dependencies

### hardware

- [lunanode](https://lunanode.io)
Lunanode is a cloud resource provider which is used to setup your satoshipay server.

- Custom:
    - 1-4GB RAM
    - 25-420 GB HDD/SSD
    - 1-2 CPUS

### software

- [cyphernode](https://cyphernode.io)

cyphernode is containerized network of applications that provide the basis to build bitcoin infrastructure. It is designed with [bitcoin-core](https://bitcoin.org) at the center, running as a peer on the bitcoin network and managing all transactions related to its registered public keys. Other `cypherapps` can connect to the `cyphernodenet` which is the encrypted docker overlay network that together makes up your infrastructure.

- [satsbank](https://satsbank.io) 

The admin application used by vendors to manage their business accounts. Multiple users can be setup. It can be accessed at a domain hosted on lunanode. It is a Vanilla [html,css,js] web client, and a light-weight [rust] server. The backend also exposes an http api that mimicks core rpc with additional muliti-factor authentication. This can easily be integrated into your websites. For physical shops, addresses and qr codes can be printed from the admin panel with custom invoicing metadata.

It focusses on being a direct (retain the original rpc api) interface to your full-node via the bitcoin-core rpc with the addition of modular multi-factor authentication for permissioned access. If a vendor decides not use a full-node, it can run a light weight `bdk` based wallet which connects to blockstream's full-node.

It also focusses on being a watch-only wallet first. It is designed to work best with `trezor`, `bitbox` or `coldcard`.

- [specter](https://specter.solutions) (optional)

A wallet for a vendor to manage their private accounts.

- [bdk](https://bitcoindevkit.com) (custom) 

bdk is an example of a great tool to write extensions to `satoshipay` since satsbank also uses bdk for its native wallet. `bdk-cli` is also bundled as a `cypherapp` for new users to get their feet wet and explore the possibilities with the `bdk` library.


## flow 

### deploy 

> Define requirements and deploy resources

- Fill out basic merchant information in `deploy.json`

- Setup hardware wallet.

- Export your public key from your hardware wallet and complete `bitcoin.public_key` in `deploy.json`

[Setup Lunanode Account](https://dynamic.lunanode.com/)

[Setup LunaNode API Credentials](https://dynamic.lunanode.com/panel/api)

- Add `server.api_key` and `server.api_id` to `deploy.json`

- Setup SSH Key: `ssh-keygen`

[Upload SSH Public Key to Lunanode](https://dynamic.lunanode.com/panel/key)

[Setup DNS with Lunanode](https://dynamic.lunanode.com/panel/dns)

- Add `server.ssh_id` to `deploy.json`

- Add `server.host` and `server.subdomain` to  specify where to host satspay.

- Run `deploy.sh`

### configure

> Configure resources to serve specific client

- SSH  into satoshipay server and run satoshipay/configure/config.sh 

- This will require setting an admin username and password, also used by the owner to access the admin panel

- If callback_urls are auth protected, custom additions to cyphernode notifier must be made. 

- Update A Records for `host` and `subdomain` if youre not using lunanode as a DNS

### monitor

> Provide client access to services

- Visit `subdomain.host.tld`

# support: 

### Please open issues, PR's or send me an email

##### vishalmenon.92@gmail.com