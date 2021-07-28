# Getting started

Setting up you VS Code

I would propose the following extensions:

- Auto Close Tag
- Auto Rename Tag
- CodeMetrics
- Git Blame
- Git Lens
- Live Share
- Prettier
- Rainbow Brackets
- SCS IntelliSense
- solidity

- TSLint
- Visual Studio IntelliCode

## Installing

install node so you automatically get npm as your package manager

whenever you get an error, try finding out the main message and then google it

Also, check the docs of the software you are installing. Normally its a good documentation and they have probably an answer to the problems you will encounter.

before installing packages that you need for `contracts`or `backend`remeber to init the node module, so the packages can be saved with `npm init`

you should also create a `.gitignore`file where you add the node_modules that are created as this takes a lot of time to be uploaded and downloaded. And they are anyways newly created everytime you write `npm i`wichc you do after adding a new package....

## What do you need ot install

writing g in front of a package means, that you are installing it globaly. This makes sense for software you are going to want to use more often. Ans also when you want to use their command line interface (CLI).

DON'T install truffle gloably, it will likely lead to version problems

- koa
  `npm i -g koa`

* heroku CLI
  for Mac:
  `brew tap heroku/brew && brew install heroku`

## set up project

- start a project

`truffle unbox metacoin`

then your folder looks like this

```
contracts/: Directory for Solidity contracts
migrations/: Directory for scriptable deployment files
test/: Directory for test files for testing your application and contracts
truffle-config.js: Truffle configuration file
```

## Backend

go into the `backend`dir and

`npm init``

add a `server.js`and a `rouer.js`file.
add a directory for `images` and a token.json file

```
touch server.js
touch rouer.js
touch token.json
mkdir images


npm install @koa/cors --save
npm install @koa/router --save
npm install koa-static
npm i

```

login into heroku (make sure you have the heroku CLI installed before)
`heroku login`

create a new projec with heroku
`heroku create`

add the url of your app to your tokens.json file like this to the image (we are going to add the specific ID of the image later)

```
      {
         "0": {
            "name": "NFT test",
            "description": "This is the greates NFT ever",
            "image": "https://stark-hamlet-90121.herokuapp.com"
         }
      }
```

now you commit your current state to git and then you can deploy the current state on heroku

to check if it worked you can du a `curl`request like this

`curl https://stark-hamlet-90121.herokuapp.com`

you should now see the same data as in your `tokens.json` file

if VS Code propses an extension for solidity, you should do it. It makes your code way more readableI am using he first one that is called `solidity`by Juan Blanco.

## SmartContract

first when you are in the main directory of the truffle project to save your toher packages you need to initialize the package manager
`npm init`

solidity
`npm install solc`

For security and ERC721 standards we need this library
`npm install @openzeppelin/contracts`

- always add the licence in the first line of your contract/ Solidity File
  `// SPDX-License-Identifier: MIT`

- it might be that your source file require a differnet compiler version
- [solution for windowsOS](https://medium.com/blockchangers/how-to-fix-your-truffle-and-solidity-versioning-with-npx-from-npm-51b5fcb0825f)

add

```
   compilers: {
      solc: {
         version: "0.8.0",    // Fetch exact version from solc-bin (default: truffle's version)
         // docker: true,        // Use "0.5.1" you've installed locally with docker (default: false)
         // settings: {          // See the solidity docs for advice about optimization and evmVersion
         //  optimizer: {
         //    enabled: false,
         //    runs: 200
         //  },
         //  evmVersion: "byzantium"
         // }
      }
   },
```

to your `truffle-config.js`file

and write in the second line of each smart contract
`pragma solidity >= 0.6.0;`

to configure you app to connect to a testnet you need to add a hdwalletprovider to your config file
first enter in the terminal

so as you already got node.js make sure to install `web3.js` as well

`npm install web3`

then you can install the HDWallet Provider

`npm install @truffle/hdwallet-provider`

the requirements for this are

```
Node >= 7.6
Web3 ^1.2.0
```

so as you already got node.js make sure to install `web3.js` as well

`npm install web3`

then you need to add this informaiton to the header of your `tuffel-config.js` file should look like this:

```
1. const HDWalletProvider = requie('@truffle/hdwalletprovider');
2. const mnemonic = 'Amphibious Witches Relished Sour Bacon Wholeheartedly However Mosquitoes Circulated Invisible Skirts Boorishly';
```

create your own mneomic scentence. (you can do it online for teststuff but I guess when you go real it should be safe)

```

Warning: In production, we highly recommend storing the mnemonic in another (secret) file, to reduce the risk of the mnemonic becoming known. If someone knows your mnemonic, they have all of your addresses and private keys!

If you would use privae keys:


NOTE: This is just an example. NEVER hard code production/mainnet private keys in your code or commit them to git. They should always be loaded from environment variables or a secure secret management system.
```

then you want to add to the `module.exports`in the `truffle-config.js` the Rinkeby test network

```

  contracts_build_directory: './forntend/scr/contracts', // this will connect us to the frontend
  networks: {
    //  development: {
    //    host: "127.0.0.1",
    //    port: 7545,
    //    network_id: "*"
    //  },
    //  test: {
    //    host: "127.0.0.1",
    //    port: 7545,
    //    network_id: "*"
    //  }

    rinkeby: {
      provider: () => new HDWalletProvider(
        mnemonic,
        // here you add the url to a infura node. For that you need to create an account in infura and then create a project there.
        // In the settings of the Infura project you need to choose as an enpoint the rinkeyby tesnet and then take the key and add it here as URL
        'https://rinkeby.infura.io/v3/1ee87164e7b1448daed738352cb48e5d',
        0,
        1 // generate one address from this mnemonic
      ),
      network_id: 4, // rinkeby
      skipDryRun: true
    }
  }
```

[Here](https://www.trufflesuite.com/guides/using-infura-custom-provider) you can find more info on how to connect your Dapp createt with the truffel framework to a testnet with infura.

to deploy the contract to rinkeby testnetwork
`truffle migrate --reset --network rinkeby`

and here i am Stuck... So far.

but it works and when we compile the project truffel framework creates a folder for the contracts that you can find here `frontend/scr/contracts`
and in the file with the same name as our smart contract we can find the deployment adress inside to connect our forntend to the smart contract

unfortunately it is not super smart so it might create a second src folder next to your Vue project and then you will have to move the contracts folder int he other folder where your `App.js` file lies

## Frontend

set up the Vue project
`vue create frontend`

For this tutorial you should choose the default for a small app

but if you want to choose manually (this is just how I like to set up my projects.. but it will save you some time.. )
