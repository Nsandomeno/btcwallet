# Steps

# Start BTCD
Set btcd.conf

```
[Application Options]
testnet=1
nolisten=0
rpcuser=na-dev
rpcpassword=password123
```

Set btcctl.conf
```
[Application Options]
rpcuser=na-dev
rpcpassword=password123
```

Move the sample configs into place if not done manually.

Move the Btcd instance config file from this repository
`cp local-btcd.conf ~/Library/Application\ Support/Btcd/btcd.conf`

Move the Btcctl config file from this repository
`cp local-btcctl.conf ~/Library/Application\ Support/Btcctl/btcctl.conf`

Move the Btcd TLS Certificate into the Btcwallet data directory
`cp ~/Library/Application\ Support/Btcd/rpc.cert ~/Library/Application\ Support/Btcwallet/btcd.cert`

Move the Btcd TLS Certificate into the BtcwalletClient data directory
`cp ~/Library/Application\ Support/Btcd/rpc.cert ~/Library/Application\ Support/Signerclient/btcd.cert`

# (1) Build

`make build`

# (2) Server - Configure
Create a `.btcwallet` at the root of your OS' filesystem. There is an 
example for the server at the root of this repository.

`mkdir ~/.btcwallet`

`cp local-server.conf ~/.btcwallet/btcwallet.conf`

MacOS
`cp local-server.conf ~/Library/Application\ Support/Btcwallet/btcwallet.conf`

# (2) Client - Configure
Need a separate directory to run a client of the wallet locally. Do this at the root of your OS' filesystem as well. Similarly, there is an example .conf for the client of the wallet at the root of this repository.

`mkdir ~/.signer-client`

`cp local-client.conf ~/.signer-client/btcwallet.conf`

MacOS

`cp local-client.conf ~/Library/Application\ Support/Signerclient/btcwallet.conf`

Copy Wallet Server RPC.cert
`cp ~/Library/Application\ Support/Btcwallet/rpc.cert ~/Library/Application\ Support/Signerclient/rpc.cert`

Copy the BTCD RPC.cert
`cp ~/Library/Application\ Support/Btcd/rpc.cert ~/Library/Application\ Support/Signerclient/btcd.cert`

# (3) Run Server
Create a new wallet (only needed on instance creation)
`btcwallet --configfile=< Config file Path > --create`

Run btcwallet
`btcwallet --configfile=< Config file Path >`

Record the private passphrase
EX: `password123`

Record the wallet generation seed
EX: `dba5f7beca401b18715a36774e64cdf737008cc8492c2c0fa7107c096e7de802`

# (4) Test the Connection from Client to Server
Run btcwallet-client
`go run ./cmd/mvp-remote-sign-demo/main.go`