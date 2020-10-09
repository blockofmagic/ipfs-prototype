## Installation

### Install Geth

```bash
$ sudo yum install golang
$ sudo yum install gmp-devel

$ git clone https://github.com/ethereum/go-ethereum && cd go-ethereum
$ make geth
$ cp build/bin/geth /usr/bin/.
```
### Install IPFS
```bash
$ wget https://dist.ipfs.io/go-ipfs/v0.7.0/go-ipfs_v0.7.0_linux-amd64.tar.gz
$ tar -xvzf go-ipfs_v0.7.0_linux-amd64.tar.gz
$ cd go-ipfs
$ sudo ./install.sh
```

## Setup
### Setup blockchain with geth
Create a new directory for your private blockchain. In your terminal (Mac/Linux) or command prompt (Windows) window, navigate to the directory and create a new account:

```bash
$ geth --datadir="./" account new
```
Enter a password when prompted for your local Ethereum account. Geth will create a keystore directory and store the account file in the keystore.

### Setup Genesis Block

Setting up a private blockchain requires defining a genesis block, which sets the initial parameters and token distribution.

In the directory containing your account, copy/paste/save the following JSON into a file called genesisblock.json:
```json
{
    "config": {
        "chainID"       : 10,
        "homesteadBlock": 0,
        "eip150Block":    0,
        "eip155Block":    0,
        "eip158Block":    0
    },
    "nonce": "0x01",
    "difficulty": "0x20000",
    "mixhash": "0x00000000000000000000000000000000000000647572616c65787365646c6578",
    "coinbase": "0x0000000000000000000000000000000000000000",
    "timestamp": "0x00",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x00",
    "gasLimit": "0x2FEFD8",
    "alloc": {
    }
}
```

This will be block 0 of your private blockchain. If you ever wish to have others join this network, they will need this genesis block as well.

We will now instantiate the blockchain network and load the geth console:
```bash
geth --datadir="./" init genesisblock.json
geth --datadir="./" --networkid 23422  --rpc --rpccorsdomain="*" --rpcport="8545" --minerthreads="1" --mine --nodiscover --maxpeers=0 --unlock 0 console --allow-insecure-unlock

### Setup IPFS
```bash
$ ipfs init
$ ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin '["http://localhost:3000", "https://webui.ipfs.io", "http://127.0.0.1:5001"]'
$ ipfs config --json API.HTTPHeaders.Access-Control-Allow-Methods '["POST"]'
```
```
