## Get docker image
Please download the docker image from [here](https://hub.docker.com/r/apronnetwork/apron-node/).

## Get docker compose file
Please download the docker compose file from [here](https://github.com/Apron-Network/apron-node/blob/upgrade_contract/scripts/docker-compose-base.yml)

## Start apron-node and frontend service

```
docker-compose -f docker-compose-base.yml up -d
```

## Access frontend service
Open the browser and go to [http://127.0.0.1:3001](http://127.0.0.1:3001).

## Set custom point

set custom point to `ws://127.0.0.1:9944`

## Add account 

please use this **Raw seed** `0xe40891ed4fa2eb6b8b89b1d641ae72e8c1ba383d809eeba64131b37bf0aa3898` 

The account must be `5F7Xv7RaJe8BBNULSuRTXWtfn68njP1NqQL5LLf41piRcEJJ`

![Add Account](https://github.com/Apron-Network/apron-node/blob/upgrade_contract/scripts/images/add_acount.png)

## Transfer some tokens to the added account.

## Download the contracts
please download the contracts from [here](https://github.com/Apron-Network/apron-gateway-rust/tree/main/release)

## Upload and deploy market contract
Please ensure the controller is `5F7Xv7RaJe8BBNULSuRTXWtfn68njP1NqQL5LLf41piRcEJJ`

![Market Contract](https://github.com/Apron-Network/apron-node/blob/upgrade_contract/scripts/images/market_contract.png)

## Upload and deploy stats contract
1. Please ensure the controller is `5F7Xv7RaJe8BBNULSuRTXWtfn68njP1NqQL5LLf41piRcEJJ`
2. Please ensure the market addr is the address of market contract created above.


