# satoshipay

The goal of `satoshipay` is to provide a plug and play orchestration of custom bitcoin infrastructure for individuals/merchants to manage bitcoin accounts for their physical or online businesses.

It provides a suite of open source software with accompanying deployment, configuration and monitoring applications and scripts. 

## goals

Users:
- freedom maximizing

Admins: 
- secure, light-weight & extendable

Community:
- public standardized sound money tooling

## specifications

- bitcoin-only
- satoshi units
- 

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

The admin application used by vendors to manage their business accounts with multi user access control. It is a Vanilla [html,css,js] web client, and a light-weight [rust-warp](https://github.com/seanmonstar/warp) server and [rust-sled](https://github.com/spacejam/sled) database. The server exposes a http api that mimicks core rpc with additional muliti-factor authentication. It also exposes a simple bdk wallet api for the option to run without a local node. This api can easily be integrated into your websites like traditional payment gateway apis. For physical shops, addresses and qr codes can be printed from the admin panel with custom invoicing metadata.

It also focusses on being a watch-only wallet first. It is designed to work best with `trezor`, `bitbox` or `coldcard`.

- [specter](https://specter.solutions) (optional)

A wallet for a vendor to manage their private accounts.

- [bdk](https://bitcoindevkit.com) (custom) 

bdk is an example of a great tool to write extensions to `satoshipay` since satsbank also uses bdk for its native wallet. `bdk-cli` is also bundled as a `cypherapp` for new users to get their feet wet and explore the possibilities with the `bdk` library.

- [localbitcoins-api](https://api.localbitcoins.com) (custom)

LBC is a peer-to-peer bitcoin exchange that exposes a simple api to buy and sell Bitcoin against local currencies. Vendors can easily plug-in with a custom LBC `cypherapp` to manage their LBC account and setup a sell schedule when fiat is required to pay local bills.

## flow 

### deploy 

> Define resource requirements and deploy

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

> Configure infrastructure and applications according to client specifications

- SSH  into satoshipay server and run satoshipay/configure/config.sh 

- This will require setting an admin username and password, also used by the owner to access the admin panel

- If callback_urls are auth protected, custom additions to cyphernode notifier must be made. 

- Update A Records for `host` and `subdomain` if youre not using lunanode as a DNS

### monitor

> Monitor infrastructure and use applications

- Visit `subdomain.host.tld`

# support: 

### Please open issues, pull requests or send me an email

##### vishalmenon.92@gmail.com
