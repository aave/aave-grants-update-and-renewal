```
        .///.                .///.     //.            .//  `/////////////-
       `++:++`              .++:++`    :++`          `++:  `++:......---.`
      `/+: -+/`            `++- :+/`    /+/         `/+/   `++.
      /+/   :+/            /+:   /+/    `/+/        /+/`   `++.
  -::/++::`  /+:       -::/++::` `/+:    `++:      :++`    `++/:::::::::.
  -:+++::-`  `/+:      --++/---`  `++-    .++-    -++.     `++/:::::::::.
   -++.       .++-      -++`       .++.    .++.  .++-      `++.
  .++-         -++.    .++.         -++.    -++``++-       `++.
 `++:           :++`  .++-           :++`    :+//+:        `++:----------`
 -/:             :/-  -/:             :/.     ://:         `/////////////-
```
# Aave-Grants-Update-and-Renewal

1. Complete .env file with environment variables. Make sure to include `MAINNET_FORK="true"`
2. Review `tasks/proposal/grants-dao-proposal`
3. Run: `npm install`
4. Run: `npm run hardhat grants-dao-proposal`

# Aave Smart Contract Template Repo

This repository is set up to be a starting point for smart contract repos.

# Documentation

## Setup

- Clone the repo
- run `npm install`

Follow the next steps to setup the repository:

- Install `docker` and `docker-compose`
- Create an enviroment file named `.env` and fill out the environment variables per `.env.example`

## Running in Docker

Terminal Window 1
`docker-compose up`

Once Terminal Window 1 Loaded - in a seperate terminal window - Terminal Window 2: 
`docker-compose exec contracts-env bash`

In Terminal Window 2, run desired scripts from npm package file (i.e `npm run hardhat compile`)

## Available Networks

- `Hardhat` - use `npm run hardhat $insert_command`
- `Hardhat - Mainnet fork` - set MAINNET_FORK in env file to "true" and use `npm run hardhat $insert_command`
- `Kovan` - use `npm run hardhat:kovan $insert_command`
- `Ropsten` - use `npm run hardhat:ropsten $insert_command`
- `Mainnet` - use `npm run hardhat:main $insert_command`
- `Mumbai` - use `npm run hardhat:mumbai $insert_command`
- `Matic` - use `npm run hardhat:matic $insert_command`
- `Tenderly` - use `npm run hardhat:tenderly`

## Available Tasks

- `get-info` - this will print current chain info: ChainId, Current Block, Balance of a hardcoded address
- `print-default-wallets` - print the wallets available based on the .env secrets
- `deploy` - generic deployment task
- `verify` - verifies contract on Etherscan
- `verify-template` - template verification helper

Note:

When using the tasks through `npm run hardhat <taskname>` if you are including options you will need to include and extra -- prior to the task options. Example of task with options:

```
npm run hardhat deploy -- --contract Greeter --printparams
```

### deploy

Usage: hardhat [GLOBAL OPTIONS] deploy --contract <STRING> --libraries <STRING> --librariesfile <STRING> --params <STRING> --paramsfile <STRING> [--printparams] --signer <STRING> [--verify]

OPTIONS:

  --contract     	Name of contract to deploy
  --libraries    	json as string mapping of libraries to address
  --librariesfile	file containing mapping of libraries to address
  --params       	JSON string of contract params - defaults to CLI
  --paramsfile   	Path to a TS file with params defined as default export
  --printparams  	Print constructor params
  --signer       	Define signer - private key(pk), mnemonic(mn), defender(ozd) - defaults to ethers signer
  --verify       	Verify contract on Etherscan

deploy: deploy contract - add contract name and params as arguements

The parameters for the contract constructor can be set four different ways:
1. use the option `--params` as a stringified JSON
2. use the option `--paramsfile` to define the path to a ts file that has the parameters as the default export
2. hardcode the params as a JSON in the contractparams variable in the deploy task
    - you can use the --printparams option to get a template JSON of the params to copy and paste into the script and fill out 
3. use the cli. By not setting contractparams you can 

To include the contract params as a string, pay close attentions to the quotations used to create the stringified JSON object. Below is a working example:

```
npm run hardhat deploy -- --contract Greeter --params '{"greeting": "asdf","testNumber": 12, "testAddress": "0x3619DbE27d7c1e7E91aA738697Ae7Bc5FC3eACA5"}'
```

Example using --paramsfile
```
npm run hardhat deploy -- --contract Greeter --paramsfile ./greeterParams.ts
```

## verify-template

Usage: hardhat [GLOBAL OPTIONS] verify-template --contract <STRING> --contractaddress <STRING> --libraries <STRING> --librariesfile <STRING> --params <STRING> --paramsfile <STRING> [--printparams]

OPTIONS:

  --contract       	Name of contract to deploy
  --contractaddress	Address of deployed contract to verify
  --libraries      	json as string mapping of libraries to address
  --librariesfile  	file containing mapping of libraries to address
  --params         	JSON string of contract params - defaults to CLI
  --paramsfile     	Path to a TS file with params defined as default export
  --printparams    	Print constructor params

verify-template: verify contract on etherscan

This wraps the default 'verify' task to enable some flexibility in how params and libraries are provided.

## Tenderly Fork

Step 1 - Set up Tenderly Authorization per the usage section of their site:

https://www.npmjs.com/package/@tenderly/hardhat-tenderly

Step 2 -
Set the related variables in the .env file to work with a tenderly fork. If you are using a shared project - use the company name and the project name for Username and Project.

Step three - use `--network tenderly` in your hardhat commands
