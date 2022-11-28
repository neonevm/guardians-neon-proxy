## Operator read-only mode using docker-compose.

### Requirements

Please use at least version v2.12.1 for docker-composer, following instructions from [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

- Docker engine should follow [official docs](https://docs.docker.com/engine/install/). In this page, there are install procedures for all Linux distros.

- Docker-compose is required to run yaml file: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

### Hardware specs

Server (cloud/virtual machine) with 4vCPU and 8GB RAM - 500GB of disk.
Linux ubuntu/centos based OS.

### Instructions

First of all, you should have your RPC node endpoint.

You can define it on install.sh script, example:

The current version is v0.14.1, but you can just replace with any specific version with 

```bash
REVISION="stable"

```

```bash
sudo SOLANA_URL="http://solana.rpc.node/9805237840987435" REVISION="v0.14.1" docker-compose -f docker-compose-operator-ro.yaml up -d 

```
This docker composer will use your local disk as storage for postgresql database:

```bash
volumes:
      - db:/var/lib/postgresql/data
```

The db scheme is related to local driver from docker daemon:

```bash
volumes:
  db:
    driver: local

```


### Environments

Some container environments need attention for production, such as:

```bash
      POSTGRES_DB: neon-db
      POSTGRES_USER: neon-proxy
      POSTGRES_PASSWORD: neon-proxy-pass
      POSTGRES_HOST: postgres
```

For read-only mode,   ``` ENABLE_SEND_TX_API: "NO" ``` should stay as "NO" for correct usage. This is how application works without operator-keys.



##### PYTH_MAPPING_ACCOUNT

The ```PYTH_MAPPING_ACCOUNT``` environment follow the current structure from https://pyth.network/developers/accounts website:

- For devnet: ```PYTH_MAPPING_ACCOUNT=¨BmA9Z6FjioHJPpjT39QazZyhDRUdZy2ezwx4GiDdE2u2¨```

- For testnet: ```PYTH_MAPPING_ACCOUNT=¨AFmdnt9ng1uVxqCmqwQJDAYC5cKTkw8gJKSM5PnzuF6z¨```

- For mainnet-beta: ```PYTH_MAPPING_ACCOUNT=¨AHtgzX45WTKfkPG53L6WYhGEXwQkN1BVknET3sVsLL8J¨```


##### EVM_LOADER

The ```EVM_LOADER``` environment follow the current structure:

- For devnet: ```EVM_LOADER=¨eeLSJgWzzxrqKv1UxtRVVH8FX3qCQWUs9QuAjJpETGU¨```

- For testnet: ```EVM_LOADER=¨eeLSJgWzzxrqKv1UxtRVVH8FX3qCQWUs9QuAjJpETGU¨```

### Install script

Just run ```./install.sh``` and check your containers logs.

```bash

#docker logs -f proxy --tail 10

2022-11-25 12:07:19.294 I run-proxy.sh:3 1 Proxy:StartScript {} Start Proxy service
2022-11-25 12:07:19.296 I run-proxy.sh:5 1 Proxy:StartScript {} Init environment set
Config File: /root/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com 
WebSocket URL: ws:https://api.devnet.solana.com
Keypair Path: /root/.config/solana/id.json 
Commitment: confirmed 
2022-11-25 12:07:19.303 I run-proxy.sh:7 1 Proxy:StartScript {} run-proxy


```

The endpoint [http://127.0.0.1:9090/solana](http://127.0.0.1:9090/solana) can be used in your local metamask for testing purposes.






