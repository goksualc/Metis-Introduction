# Running a Metis Replica Node


## Requirements

- Linux(x86_64)
- docker 

Check the 'metis-replica-node'. First step is forking the repository below 

```
git clone https://github.com/ericlee42/metis-replica-node
```

You can find necessary instruction inside the repo. 

Need to warn macOS users for the errors that they'll face below. You can face an error like this if you are using Apple Silicon M1 or M2 chip.

```yaml
docker compose up -d
[+] Running 0/1
 ⠦ dtl Pulling                                                             2.6s 
no matching manifest for linux/arm64/v8 in the manifest list entries

platform: linux/amd64
```

You should add platform type of to the docker-compose.yml docker-compose-testnet.yml docker-compose-mainnet.yml

```yaml
services:
  dtl:
    image: metisdao/data-transport-layer:20230713210754
    platform: linux/amd64
```

best part of running a node how to get the data from replia node?

## Get the Block Number
Returns the current block number.

```console
curl -sS 'https://andromeda.metis.io' --data-raw '{"id":"1","jsonrpc":"2.0","method":"eth_blockNumber","params":[]}' -H 'Content-Type: application/json'  | jq -r '.result' | xargs printf '%d\n'
```

example output: 
```console
13226810
```

## Get the Network ID
Returns the current network id.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"net_version",
	"params":[],
	"id":67
}'
```

example output: 
```console
{"jsonrpc":"2.0","id":67,"result":"1088"}
```

## Get Network Connection
Returns true if client is actively listening for network connections.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"net_listening",
	"params":[],
	"id":67
}'
```

example output:
```console
{"jsonrpc":"2.0","id":67,"result":true}
```

## peerCount
Returns number of peers currently connected to the client.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"net_peerCount",
	"params":[],
	"id":74
}'
```

example output:
```console
{"jsonrpc":"2.0","id":74,"result":"0x0"}
```

## hashRate
Returns the number of hashes per second that the node is mining with.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"eth_hashrate",
	"params":[],
	"id":71
}'
```

example output:
```console
{"jsonrpc":"2.0","id":71,"result":"0x0"}
```

## Accounts
Returns a list of addresses owned by client.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"eth_accounts",
	"params":[],
	"id":1
}'
```

example output:
```console
{"jsonrpc":"2.0","id":1,"result":["0x00000398232e2064f896018496b4b44b3d62751f"]}

```

## getBalance
Returns the balance of the account of given address.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"eth_getBalance",
	"params":[
		"0x4200000000000000000000000000000000000007", 
		"latest"
	],
	"id":1
}'
```

example output:
```console
{"jsonrpc":"2.0","id":1,"result":"0x0"}
```

You can check the balance of the account from here 

```
https://explorer.metis.io/address/0x00000398232e2064f896018496b4b44b3d62751f 
```

## getTransactionCount

Returns the number of transactions sent from an address.

```console
curl --location 'https://andromeda.metis.io/' \
--header 'Content-Type: application/json' \
--data '{
	"jsonrpc":"2.0",
	"method":"eth_getTransactionCount",
	"params":[
		"0x407d73d8a49eeb85d32cf465507dd71d507100c1",
		"latest"
	],
	"id":1
}'
```

example output:
```console
{"jsonrpc":"2.0","id":1,"result":"0x0"}
```