# Diffyscan

![python >=3.10,<4](https://img.shields.io/badge/python-≥3.10,<4-blue)
![poetry ^1.8](https://img.shields.io/badge/poetry-^1.8-blue)
![license MIT](https://img.shields.io/badge/license-MIT-brightgreen)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

Diff your Ethereum smart contracts code from GitHub against Blockchain explorer verified source code.

Supports reformatting solidity code by means of prettifier solidity plugin before comparing the sources (option `--prettify`).

## Install

```bash
pipx install git+https://github.com/lidofinance/diffyscan
```

If need `--prettify` option

```shell
npm install
```

## Usage

Set your Etherscan token to fetch verified source code,

```bash
export ETHERSCAN_EXPLORER_TOKEN=<your-etherscan-token>
```

Set your Github token to query API without strict rate limiting,

```bash
export GITHUB_API_TOKEN=<your-github-token>
```

Start script with one of the examples provided (or entire folder of configs)

```bash
diffyscan config_samples/lido_dao_sepolia_config.json
```

Alternatively, create a new config file named `config.json`,

```json
{
    "contracts": {
        "0x28FAB2059C713A7F9D8c86Db49f9bb0e96Af1ef8": "OssifiableProxy",
        "0xDba5Ad530425bb1b14EECD76F1b4a517780de537": "LidoLocator"
    },
    "explorer_hostname": "api-holesky.etherscan.io",
    "explorer_token_env_var": "ETHERSCAN_EXPLORER_TOKEN",
    "github_repo": {
        "url": "https://github.com/lidofinance/lido-dao",
        "commit": "cadffa46a2b8ed6cfa1127fca2468bae1a82d6bf",
        "relative_root": ""
    },
    "dependencies": {
        "@openzeppelin/contracts-v4.4": {
            "url": "https://github.com/OpenZeppelin/openzeppelin-contracts",
            "commit": "6bd6b76d1156e20e45d1016f355d154141c7e5b9",
            "relative_root": "contracts"
        }
    }
}
```

Start the script

```bash
diffyscan
```

> Note: Brownie verification tooling might rewrite the imports in the source submission. It transforms relative paths to imported contracts into flat paths ('./folder/contract.sol' -> 'contract.sol'), which makes Diffyscan unable to find a contract for verification.

For contracts whose sources were verified by brownie tooling:

```bash
diffyscan --support-brownie
```

ℹ️ See more config examples inside the [config_samples](./config_samples/) dir.

## Development setup

### Prerequisites

This project was developed using these dependencies with their exact versions listed below:

- Python 3.12
- Poetry 1.8
- if need `--prettify` option support:
  - npm

Other versions may work as well but were not tested at all.

### Setup

1. Install Poetry

Use the following command to install poetry:

```bash
pip install --user poetry~=1.8
```

alternatively, you could proceed with `pipx`:

```bash
pipx install poetry~=1.8
```

2. Activate poetry virtual environment,

```bash
poetry shell
```

3. Install [poetry-dynamic-versioning](https://github.com/mtkennerly/poetry-dynamic-versioning?tab=readme-ov-file#installation)

- In most cases: `poetry self add "poetry-dynamic-versioning[plugin]"`
- If you installed Poetry with Pipx: `pipx inject poetry "poetry-dynamic-versioning[plugin]"`

4. Install Python dependencies

```bash
poetry install
```

5. If need `--prettify` option

```shell
npm install
```
