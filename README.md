# Manta Pacific Token List

This repository maintains a list of ERC20 tokens available on Manta Pacific. The list is kept updated by the community.

If you want to add a token or validate an addition, please follow the procedures outlined below.

## How to add a Token (for community)

IMPORTANT: Before adding a new token, it is mandatory to verify the token's smart contract. This ensures the authenticity and security of the token. Contract verification should be done through [Manta Pacific Explorer](https://pacific-explorer.manta.network/) or [Etherscan's](https://etherscan.io/) contract verification tools.

To add a new Token,

1. `Fork` this repository to your own GitHub account, then `clone` your fork and create a new branch.

Example:

```
git clone https://github.com/<your-github-username>/manta-pacific-token-list.git
cd manta-pacific-token-list
git checkout -b feat/<token-name>
```

2. Fill out the [./json/manta-pacific-mainnet-token-list.json](./json/manta-pacific-mainnet-token-list.json) with your token's information.

Example:

```json
"tokens": [
  {
    "chainId": 169,
    "chainURI": "https://pacific-explorer.manta.network/block/0",
    "tokenId": "https://pacific-explorer.manta.network/address/0x1c466b9371f8aBA0D7c458bE10a62192Fcb8Aa71",
    "tokenType": ["canonical-bridge"],
    "address": "0x1c466b9371f8aBA0D7c458bE10a62192Fcb8Aa71",
    "name": "Dai Stablecoin",
    "symbol": "DAI",
    "decimals": 18,
    "createdAt": "2023-11-27",
    "updatedAt": "2023-11-27",
    "logoURI": "https://s2.coinmarketcap.com/static/img/coins/64x64/4943.png",
    "extension": {
      "rootChainId": 1,
      "rootChainURI": "https://etherscan.io/block/0",
      "rootAddress": "0x6B175474E89094C44Da98b954EedeAC495271d0F"
    }
  }
]
```

Description of the fields:

| Name         | Description                                                                                                                                                         | type    | Required?                                                   |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ----------------------------------------------------------- |
| chainId      | The typically used number identifier for the chain on which the token was issued                                                                                    | number  | Mandatory                                                   |
| chainURI     | A resolvable URI to the genesis block of the chain on which the token was issued following the RFC 3986 standard                                                    | string  | Mandatory                                                   |
| tokenId      | A resolvable URI of the token following the RFC 3986 standard to for example the deployment transaction of the token, or a DID identifying the token and its issuer | string  | Mandatory                                                   |
| tokenType    | Describes the type of token (eg: `canonical-bridge`, `bridge-reserved`, `external-bridge`, `native`), see details bellow.                                           | string  | Mandatory                                                   |
| address      | Address of the token smart contract                                                                                                                                 | string  | Mandatory                                                   |
| name         | Token name                                                                                                                                                          | string  | Mandatory                                                   |
| symbol       | Token symbol e.g. UNI                                                                                                                                               | string  | Mandatory                                                   |
| decimals     | Allowed number of decimals for the listed token                                                                                                                     | integer | Mandatory                                                   |
| createdAt    | Date and time token was created                                                                                                                                     | string  | Mandatory                                                   |
| updateAt     | Date and time token was last updated                                                                                                                                | string  | Mandatory                                                   |
| logoURI      | URI or URL of the token logo following the RFC 3986 standard                                                                                                        | string  | Optional                                                    |
| extension    | Extension to specify information about the token on its native chain if it was bridged                                                                              | Array   | Mandatory if the token has been bridged, otherwise optional |
| rootChainId  | The typically used number identifier for the chain on which the token was originally issued                                                                         | number  | Mandatory if the token has been bridged, otherwise optional |
| rootChainURI | A resolvable URI to the genesis block of the root chain on which the token was originally issued following the RFC 3986 standard                                    | string  | Mandatory if the token has been bridged, otherwise optional |
| rootAddress  | Address of the token on its native chain                                                                                                                            | string  | Mandatory if the token has been bridged, otherwise optional |

Token types:

- `canonical-bridge`: token originally on Ethereum, which has been bridged to Manta Pacific with <b>Manta Pacific Canonical Bridge</b>.

  <b>Example</b>: DAI on Ethereum Mainnet has this address `0x6B175474E89094C44Da98b954EedeAC495271d0F`, after being bridged on Manta Pacific it has this address `0x1c466b9371f8aBA0D7c458bE10a62192Fcb8Aa71`

- `bridge-reserved`: token reserved in the canonical bridge smart contract to prevent any bridged <b>Manta Pacific Canonical Bridge</b>.

- `external-bridge`: token bridged on another layer (Ethereum in general) and Manta Pacific using a custom protocol bridge.

- `native`: Token first created on Manta Pacific.

<b>Additional guidelines</b>:

- Please ensure the completed JSON follows the schema outlined in [./json/schema/l2-token-list-schema.json](./json/schema/l2-token-list-schema.json).
- Make sure to add the token following alphabetical order of the `symbol` field.
- Update the `updatedAt` (and potentially `createdAt`) fields for the file and the token
- Update the file version:
  - Increase `patch` when modifying information of an existing token.
  - Increase `minor` when modifying adding a new token.
  - Increase `major` when changing the structure of the file.

3. Commit your changes and push your branch.

<b>Note</b>: Only commit the list file. Do not modify the schema or the templates.

4. Go to https://github.com/Manta-Network/manta-pacific-token-list/pulls and create a new PR. Make sure to set the base branch as `main`.

