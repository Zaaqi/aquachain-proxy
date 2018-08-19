# aquachain-proxy

Aquachain mining proxy with web-interface.

**Proxy feature list:**

* Rigs availability monitoring
* Keep track of accepts, rejects, blocks stats
* Easy detection of sick rigs
* Daemon failover list

![Demo](https://raw.githubusercontent.com/sammy007/ether-proxy/master/proxy.png)

### Building on Linux

Dependencies:

  * go >= 1.4
  * geth

Export GOPATH:

    export GOPATH=$HOME/go

Install required packages:

    go get github.com/aquanetwork/aquachain/common
    go get github.com/aquanetwork/aquachain/consensus/lightvalid
    go get github.com/goji/httpauth
    go get github.com/gorilla/mux
    go get github.com/yvasiyarov/gorelic

Compile:

    go build -o aqua-proxy main.go

### Building on Windows

Follow [this wiki paragraph](https://github.com/ethereum/go-ethereum/wiki/Installation-instructions-for-Windows#building-from-source) in order to prepare your environment.
Install required packages (look at Linux install guide above). Then compile:

    go build -o aqua-proxy.exe main.go

### Building on Mac OS X

If you didn't install [Brew](http://brew.sh/), do it. Then install Golang:

    brew install go

And follow Linux installation instructions because they are the same for OS X.

### Configuration

Configuration is self-describing, just copy *config.example.json* to *config.json* and specify endpoint URL and upstream URLs.

#### Example upstream section

```javascript
"upstream": [
  {
    "pool": true,
    "name": "pool.rplant.xyz",
    "url": "http://aquapool.rplant.xyz:19998/0x892d23e26416f44e4fb32f1b10e8400b8f6cdd5f/proxy",
    "timeout": "10s"
  },
  {
    "name": "backup-aqua",
    "url": "http://127.0.0.1:8545",
    "timeout": "10s"
  }
],
```

In this example we specified [aquapool.rplant.xyz](https://aquapool.rplant.xyz) mining pool as main mining target and a local geth node as backup for solo.

With <code>"submitHashrate": true|false</code> proxy will forward <code>aqua_submitHashrate</code> requests to upstream.

#### Running

    ./aqua-proxy config.json

#### Mining

    aquacppminer -F http://x.x.x.x:8546/miner/1000000/worker

### Pools that work with this proxy

* [aquapool.rplant.xyz](https://aquapool.rplant.xyz) RU Aquachain mining pool

Pool owners, apply for listing here. PM me for implementation details.

### TODO

**Currently it's solo-only solution.**

* Report block numbers
* Report luck per rig
* Maybe add more stats
* Maybe add charts

### Donations

* **ETH**: [0xb85150eb365e7df0941f0cf08235f987ba91506a](https://etherchain.org/account/0xb85150eb365e7df0941f0cf08235f987ba91506a)

* **BTC**: [1PYqZATFuYAKS65dbzrGhkrvoN9au7WBj8](https://blockchain.info/address/1PYqZATFuYAKS65dbzrGhkrvoN9au7WBj8)

Thanks to a couple of dudes who donated some Ether to me, I believe, you can do the same.

### License

The MIT License (MIT).
