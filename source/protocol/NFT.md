# NFT

## Service Description

**Witness** is an API service provided by Nal designed to support various on-chain transaction scenarios. It is deployed in a Docker container on the user's local service, allowing users to complete on-chain operations by calling the Docker service interface. This service offers standard ERC721 and ERC1155 contracts tailored for diverse scenarios and supports token transfers for the following currencies: **ETH**, **ERC20**.

### Service Deployment

To deploy the service, please contact Nal's technical team to obtain the necessary scripts and usage instructions.

### System Configuration

- **Testing Environment**:
    - 2-core CPU, 4GB RAM, 100GB system disk
- **Production Environment**:
    - 4-core CPU, 8GB RAM, 40GB system disk
    - 100GB data disk mounted to the directory `/data`

### Required Services

- **Docker**: Install the appropriate version of Docker based on your server’s operating system.
- **Jq**: Ensure Jq is installed for JSON processing.

## Account

### Generate wallet address

#### Overview
This API generates a batch of random wallet addresses.

#### Interface URL
``` text
GET /chain/account/generateMulti
```

#### Request Parameters

count: amount of wallet address, maximum of 100 wallet addresses can be generated in one request.

``` text
/chain/account/generateMulti/{count}
```

#### Response Parameters
| Parameter | Description |
| --- | --- |
| code| Response code (e.g., N000000) |
| message| Response message (e.g., Success) |
| data| Array of wallet address data |
|&ensp;&ensp;address | Wallet address |
|&ensp;&ensp;privateKey | Wallet address private key |

#### Response Example
```json
    {
        "code": "N000000",
        "message": "Success",
        "data": [
            {
                "address": "0xcd2622da3fe4989a866093646e3b1ac661a94ff0",
                "privateKey": "a751ee6855b5d9d41138cba5d0a6f8bbf3021124e9bc928e2ca93ca096c4bed8"
            },
            {
                "address": "0xe43c69dc6f2ed50a34ec388695d387697c59acc1",
                "privateKey": "9fff3e21d782fac2021a044db1ec1748ee36f06322ce309386af721c97c78919"
            }
        ]
    }
```

### Account Transfer

#### Overview
Merchants can use this API to transfer cryptocurrency. Supported currencies include `ETH`, `ERC20`.

#### Interface URL

```text
POST /chain/account/transfer
```

#### Request Parameters

`USDT` `USDC` contractAddress: [Nal token addresses](../chain/Tokens.md#bridged-token-addresses)

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Unique request number | "1" |
| fromPK | true | String | Private key of the sender's blockchain account | "0x55879e4937981ce58d155a40e70307243524cc793003076dbfb2033fcf351632" |
| to | true | String | Target blockchain account address | "0x2ebca12753f7e9526ef76f2698b7124e37e5ce87" |
| currency | true | String | Currency type | "ETH", "ERC20" |
| contractAddress | false | String | Contract address (required for ERC20) | "0x092eA6d21145cE1093293193c3CE64D85D0904FB" |
| amount | true | String | Transfer amount | "0.05" |
| callbackUrl | false | String | URL for receiving callback notifications | "" |

#### Request Example
```json
{
    "reqNo": "1",
    "fromPK" : "0x55879e4937981ce58d155a40e70307243524cc793003076dbfb2033fcf351632",
    "to" : "0xcf028f10db66e2dac6acbfdc96aa69b031c67d37",
    "currency" : "ERC20",
    "contractAddress" : "0x092eA6d21145cE1093293193c3CE64D85D0904FB",
    "amount" : "0.000005",
    "callbackUrl" : ""
}
```
#### Response Parameters
| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000001) |
| message | Response message (e.g., Processing) |
| data |  |
|&ensp;&ensp; reqNo | Request number |
|&ensp;&ensp; txHash | Transaction hash, a unique identifier on the blockchain |

#### Response Example
```json
{
    "code": "N000001",
    "message": "Processing",
    "data": {
        "reqNo": "1",
        "txHash": "0x16d5cd8d636e9bd23bf313ac6edbe82eb89adae6d7d100448dcae73d08c2870c"
    }
}
```

### Account balance query

#### Overview
This API allows users to query the balance of an account. It supports querying for ETH, USDT, USDC, and custom ERC20 tokens.


#### Interface URL

```text
POST /chain/account/getBalance
```

#### Request Parameters

`USDT` `USDC` contractAddress: [Nal token addresses](../chain/Tokens.md#bridged-token-addresses)

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Unique request number | "1" |
| walletAddress | true | String | Blockchain account address | "0x436c39e50b40aa7c4b84326cc580b1fb4220675a" |
| currency | true | String | Currency type | "ETH", "ERC20" |
| contractAddress | false | String | ERC20 contract address if needed | "0xcb058264f2bebbc9220cdbf9dbfe55516be51d6b" (for custom ERC20) |

#### Request Example
```json
{
    "reqNo": "1",
    "walletAddress": "0x436c39e50b40aa7c4b84326cc580b1fb4220675a",
    "currency": "ERC20",
    "contractAddress": "0xcb058264f2bebbc9220cdbf9dbfe55516be51d6b"
}

```

#### Response Parameters
| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000000) |
| message | Response message (e.g., Success) |
| data |  |
|&ensp;&ensp;    balance | Account balance (up to 4 decimal places) |

#### Response Example
```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "balance": 0.0046
    }
}
```

## Token

### Mint NFT

#### Overview

This interface is used to mint an NFT.

#### Interface URL

```
POST /chain/nft/mint

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique for troubleshooting purposes | "1" |
| contractType | true | String | Contract type | "ERC721", "ERC1155" |
| nftId | true | String | Identifier for the NFT, must be unique, can be either a numeric string or a hexadecimal string starting with "0x" | "123", "0x1A" |
| amount | false | String | Number of NFTs to mint, only supports integers, required for "ERC1155" contract type | "123" |
| to | true | String | Target blockchain account address | "0x2ebca12753f7e9526ef76f2698b7124e37e5ce87" |
| password | true | String | Keystore file password | "123456" |
| callbackUrl | false | String | Service interface path to receive callback notifications |  |

#### Request Example

```json
{
    "reqNo": "1",
    "contractType" : "ERC1155",
    "nftId" : "1",
    "amount" : "100",
    "to" : "0x21dbb10c42c5caed715edf976396e1cdf7973a63",
    "password" : "123456",
    "callbackUrl" :  ""
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000001) |
| message | Response message (e.g., Processing) |
| data |  |
|&ensp;&ensp;    reqNo | Request number |
|&ensp;&ensp;    txHash | Transaction hash, unique identifier on the chain, used to query the result of the transaction |

#### Response Example

```json
{
    "code": "N000001",
    "message": "Processing",
    "data": {
        "reqNo": "1",
        "txHash": "0x16d5cd8d636e9bd23bf313ac6edbe82eb89adae6d7d100448dcae73d08c2870c"
    }
}

```



### NFT Transfer Signature

#### Overview

This interface is used to sign the transfer of an already minted NFT.

#### Interface URL

```
POST /chain/nft/sign/transfer

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique for troubleshooting purposes | "1" |
| contractType | true | String | Contract type | "ERC721", "ERC1155" |
| nftId | true | String | Identifier for the NFT, must be unique, can be either a numeric string or a hexadecimal string starting with "0x" | "123", "0x1A" |
| amount | false | String | Number of NFTs to transfer, only supports integers, required for "ERC1155" contract type | "123" |
| ownerPK | true | String | Private key of the NFT owner's blockchain account | "6f08411eb28234871c5e84d1997becd06e0bc5f6d803da8de04ccf3635ba0d7a" |
| to | true | String | Target blockchain account address | "0x2ebca12753f7e9526ef76f2698b7124e37e5ce87" |
| callbackUrl | false | String | Service interface path to receive callback notifications |  |

#### Request Example

```json
{
    "reqNo" : "1",
    "contractType" : "ERC1155",
    "nftId" : "1",
    "amount" : "50",
    "ownerPK" : "6f08411eb28234871c5e84d1997becd06e0bc5f6d803da8de04ccf3635ba0d7a",
    "to" : "0x270b739d0f7651bb05c403af0c7d4bb566111f0c",
    "callbackUrl" : ""
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000000) |
| message | Response message (e.g., Success) |
| data |  |
| &ensp;&ensp;sign | Signature |

#### Response Example

```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "sign": "0x3514dc01000000000000000000000000436c39e50b40aa7c4b84326cc580b1fb4220675a000000000000000000000000e194845303585f74a4627103a41333403ec313ee0000000000000000000000000000000000000000000000000000000005f796ef00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000046fc840f18300000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000000419f68b5f4719f8e152ac26a0e459d49e756bb8af14049a01b38e45132d03a3b472726d9fff665c8012e44d492770ffafc57646b1d0811ba546bd9921ca89dec761c00000000000000000000000000000000000000000000000000000000000000"
    }
}

```



### NFT Transfer

#### Overview

This interface is used to transfer an already minted NFT to another user.

#### Interface URL

```
POST /chain/nft/transfer

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique for troubleshooting purposes | "1" |
| contractType | true | String | Contract type | "ERC721", "ERC1155" |
| password | true | String | Keystore file password | "123456" |
| sign | true | String | Transfer signature, obtained from the NFT Transfer Signature interface |  |
| callbackUrl | false | String | Service interface path to receive callback notifications |  |

#### Request Example

```json
{
    "reqNo" : "1",
    "contractType" : "ERC1155",
    "sign" : "0x3514dc01000000000000000000000000436c39e50b40aa7c4b84326cc580b1fb4220675a000000000000000000000000e194845303585f74a4627103a41333403ec313ee0000000000000000000000000000000000000000000000000000000005f796ef00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000046fc840f18300000000000000000000000000000000000000000000000000000000000000",
    "password" : "123456",
    "callbackUrl" : ""
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000001) |
| message | Response message (e.g., Processing) |
| data |  |
| &ensp;&ensp;reqNo | Request number |
| &ensp;&ensp;txHash | Transaction hash, unique identifier on the chain, used to query the result of the transaction |

#### Response Example

```json
{
    "code": "N000001",
    "message": "Processing",
    "data": {
        "reqNo": "1",
        "txHash": "0x16d5cd8d636e9bd23bf313ac6edbe82eb89adae6d7d100448dcae73d08c2870c"
    }
}

```



### Burn NFT

#### Overview

This interface is used to burn an already minted NFT.

#### Interface URL

```
POST /chain/nft/burn

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique for troubleshooting purposes | "1" |
| contractType | true | String | Contract type | "ERC721", "ERC1155" |
| nftId | true | String | Identifier for the NFT, must be unique, can be either a numeric string or a hexadecimal string starting with "0x" | "123", "0x1A" |
| amount | false | String | Number of NFTs to burn, only supports integers, required for "ERC1155" contract type | "123" |
| ownerPK | true | String | Private key of the NFT owner's blockchain account | "6f08411eb28234871c5e84d1997becd06e0bc5f6d803da8de04ccf3635ba0d7a" |
| password | true | String | Keystore file password | "123456" |
| callbackUrl | false | String | Service interface path to receive callback notifications |  |

#### Request Example

```json
{
    "reqNo" : "1",
    "contractType" : "ERC1155",
    "nftId" : "1",
    "amount" : "50",
    "ownerPK" : "08443346e07d49a2fbb28028a0e04039febe42cf96da961b37d8269d7669c1eb",
    "password" : "123456",
    "callbackUrl" :  ""
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000001) |
| message | Response message (e.g., Processing) |
| data |  |
| &ensp;&ensp;reqNo | Request number |
| &ensp;&ensp;txHash | Transaction hash, unique identifier on the chain, used to query the result of the transaction |

#### Response Example

```json
{
    "code": "N000001",
    "message": "Processing",
    "data": {
        "reqNo": "1",
        "txHash": "0x16d5cd8d636e9bd23bf313ac6edbe82eb89adae6d7d100448dcae73d08c2870c"
    }
}

```



### Set BaseURI

#### Overview

This API allows you to set the `BaseURI`.

#### Interface URL

```
POST /chain/nft/setBaseURI

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique for troubleshooting | "1" |
| contractType | true | String | Contract type | "ERC721", "ERC1155" |
| baseURI | true | String | BaseURI for the NFT | "[http://127.0.0.1](http://127.0.0.1/)" |
| password | true | String | Keystore file password | "123456" |
| callbackUrl | false | String | URL path for receiving callback notifications |  |

#### Request Example

```json
{
    "reqNo": "1",
    "contractType": "ERC1155",
    "baseURI": "http://127.0.0.1/",
    "password": "123456",
    "callbackUrl": ""
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000001) |
| message | Response message (e.g., Processing) |
| data |  |
| &ensp;&ensp;reqNo | Request number |
| &ensp;&ensp;txHash | Transaction hash, unique identifier on the chain, used to query the result of the transaction |

#### Response Example

```json
{
    "code": "N000001",
    "message": "Processing",
    "data": {
        "reqNo": "1",
        "txHash": "0x16d5cd8d636e9bd23bf313ac6edbe82eb89adae6d7d100448dcae73d08c2870c"
    }
}

```


### Query NFT Owner

#### Overview

Query the wallet address of the NFT owner.

#### Interface URL

```
GET /chain/nft/getOwner/

```

#### Request Parameters

nftId: Minted NFT

```
/chain/query/getOwner/123

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000000) |
| message | Response message (e.g., Success) |
| data |  |
| &ensp;&ensp;owner | Owner's blockchain address |

#### Response Example

```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "owner": "0x21dbb10c42c5caed715edf976396e1cdf7973a63"
    }
}

```

### Query the Number of NFTs Owned

#### Overview

Query the number of NFTs owned by the owner.

#### Interface URL

```
POST /chain/nft/getBalanceOf

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique | "123" |
| nftId | true | String | Unique identifier of the NFT, ensure it is minted, as a numeric string or a hex string starting with "0x" | "123", "0x1A" |
| owner | true | String | Blockchain address | "0x57174e767a01e55ab2233f9c53dc6ff0c7f7d708" |

#### Request Example

```json
{
    "reqNo": "1",
    "nftId": "1001",
    "owner" : "0x57174e767a01e55ab2233f9c53dc6ff0c7f7d708"
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000000) |
| message | Response message (e.g., Success) |
| data |  |
| &ensp;&ensp;balance | Number of NFTs owned |

#### Response Example

```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "balance": "1000"
    }
}

```




### Query BaseURI

#### Overview

Retrieve the BaseURI set for different contracts, currently supporting `ERC721` and `ERC1155`.

#### Interface URL

```
POST /chain/nft/getBaseURI

```

#### Request Parameters

| Parameter | Required | Type | Description | Example |
| --- | --- | --- | --- | --- |
| reqNo | true | String | Request number, must be unique | "123" |
| contractType | true | String | Contract type: "ERC721" or "ERC1155" | "ERC1155" |
| nftId | true | String | Unique identifier of the NFT, ensure it is minted; numeric string or hex string starting with "0x" | "123", "0x1A" |

#### Request Example

```json
{
    "reqNo": "1",
    "contractType": "ERC1155",
    "nftId": "1001"
}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code, "N000000" indicates success |
| message | Response message, "Success" |
| data |  |
| &ensp;&ensp;url | BaseURI of the contract |

#### Response Example

#### ERC721

For non-fungible tokens (ERC721), replace `{nftId}` in the URL with the actual NFT ID.

```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "url": "http://127.0.0.1/{nftId}.json"
    }
}

```

#### ERC1155

For semi-fungible tokens (ERC1155), you need to append the NFT ID to the BaseURI manually.

```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "url": "http://127.0.0.1"
    }
}

```

## Common

### Query Transaction Receipt

#### Overview

This interface queries the results of transactions such as minting, transferring, burning, setting the base URI, and account transfers.

#### Interface URL

```
GET /chain/query/txReceipt/

```

#### Request Parameters

txHash: Transaction hash

```
/chain/query/txReceipt/{txHash}

```

#### Response Parameters

| Parameter | Description |
| --- | --- |
| code | Response code (e.g., N000000) |
| message | Response message (e.g., Success) |
| data |  |
| &ensp;&ensp;transactionHash | Transaction hash, same as the input parameter and in the result field |
| &ensp;&ensp;result | Transaction result |
| &ensp;&ensp;error | When the code is not N000000, this field displays the error message |

#### Response Example

A successful transaction will have a code of `N000000`.

```json
{
    "code": "N000000",
    "message": "Success",
    "data": {
        "result": {
            "blockHash": "0xd404d6157919712c374933661efe32250389575933ec6e961af03ddab4ec3858",
            "logsBloom": "0x00000000000000000000200000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000080000000000000000000000000020000000000000001000800000000000000000000000010020800000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000080000020000000200000000000000000000000000000000000000000000000000000000000",
            "transactionIndexRaw": "0x1",
            "contractAddress": null,
            "transactionIndex": 1,
            "type": "0x0",
            "transactionHash": "0x3056da3ca1f1e830d20db1c6cff3641503680a5482050c98bb62fb9993361c78",
            "gasUsed": 156030,
            "blockNumberRaw": "0x6897e",
            "blockNumber": 428414,
            "root": null,
            "statusOK": true,
            "cumulativeGasUsed": 199821,
            "from": "0x005d17a60d54c6db504daad6714d92cfdee6e353",
            "to": "0xc390702864542f4ae14b80595dc071e533a1a42c",
            "revertReason": null,
            "effectiveGasPrice": "0xf433c",
            "gasUsedRaw": "0x2617e",
            "logs": [
                {
                    "blockHash": "0xd404d6157919712c374933661efe32250389575933ec6e961af03ddab4ec3858",
                    "transactionIndexRaw": "0x1",
                    "logIndex": 0,
                    "address": "0xc390702864542f4ae14b80595dc071e533a1a42c",
                    "data": "0x",
                    "topics": [
                        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                        "0x0000000000000000000000000000000000000000000000000000000000000000",
                        "0x00000000000000000000000007788a5e634ad08cde2a5dc97c5fe13c729ff5db",
                        "0x00000000000000000000000000000000000000000000000000000000000003e9"
                    ],
                    "transactionIndex": 1,
                    "type": null,
                    "transactionHash": "0x3056da3ca1f1e830d20db1c6cff3641503680a5482050c98bb62fb9993361c78",
                    "logIndexRaw": "0x0",
                    "blockNumberRaw": "0x6897e",
                    "removed": false,
                    "blockNumber": 428414
                }
            ],
            "cumulativeGasUsedRaw": "0x30c8d",
            "status": "0x1"
        },
        "error": null,
        "transactionHash": "0x3056da3ca1f1e830d20db1c6cff3641503680a5482050c98bb62fb9993361c78"
    }
}

```