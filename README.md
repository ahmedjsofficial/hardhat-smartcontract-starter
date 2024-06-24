# Getting Started
### Step 1: Go To Infura or You can choose Node Provider
### Step 2: Add Test Ether from a Faucet
- To request funds, go to Infura Faucet↗ and sign in to acquire some tokens. Wait a few moments and your wallet should be funded!

# Step 3: Set Up Your Development Environment
To get started with the hardhat installation, we first need to set up our dev environment. To do so, create a new directory called `erc721-token-mint`

- Now, open your terminal or open your preferred code editor. And install following Packages:

```shell
npm init
npm install dotenv
npm install --save-dev hardhat @nomiclabs/hardhat-ethers ethers @openzeppelin/hardhat-upgrades @openzeppelin/contracts
```

#### Try running some of the following tasks:
```shell
npx hardhat
```
- Choose Your template to install for hardhat. I'm choosing (Typescript)
- Once your project will be created and open file `hardhat.config.js` and enjoy enviroment for smart contract.  

## Step 4: Setup Hardhat Configs
- Now, We will need a gateway to communicate to the Ethereum blockchain. Open your file: `hardhat.config.js`. As I'm using infura, I'll be infura's following configurations.
 - RPC URL: NODE_PROVIDER_NAME
 - NETWORK: CHOOSE_NETWORK
 - ACCOUNT: PRIVATE_KEY(Wallet Private Key)
```bash
/**
* @type import('hardhat/config').HardhatUserConfig
*/
require('dotenv').config();
require("@nomiclabs/hardhat-ethers");

module.exports = {
   solidity: "0.8.24",
   defaultNetwork: "sepolia",
   networks: {
      hardhat: {},
      sepolia: {
         url: "https://sepolia.infura.io",
         accounts: [`0x${process.env.PRIVATE_KEY}`]
      }
   },
}
```
- Did you notice how we are sourcing the PRIVATE_KEY variable in this file? We are loading them up from process.env using the dotenv library we installed while setting up the dev environment.

### Step 5: Write ERC-721 Smart Contract
### Step 6: Write the Compile Smart Contract
```shell
npx hardhat compile

# output
# Compiled n Solidity file successfully
```
### Step 7: Write the Deploy Script
- Now that we've got our ERC-721 contract set up, let's create the deployment script.

- Navigate to the scripts folder and create a new file called deploy.js
Open the deploy.js file and copy-paste the following code:

```bash
async function main() {
    // Grab the contract factory 
    //used to deploy new smart contracts
    const NFTDevs = await ethers.getContractFactory("NFTDevs");

    // Start deployment, returning a promise that resolves to a contract object
    const devs = await NFTDevs.deploy(); // Instance of the contract 
    console.log("Contract deployed tdevsaddress:", devs.address);
 }

 main()
   .then(() => process.exit(0))
   .catch(error => {
     console.error(error);
     process.exit(1);
   });
```
- Save and close the file
- Run npx hardhat run scripts/deploy.js --network sepolia
- Output: Contract deployed to address: 0xA2a736b9af8B2D3bb95F92d1cC015Bc6D0A2C0cB

### Step 7: Flattening the Solidity File
```shell 
npx hardhat flatten > flattened.sol
```
- This will generate a flattened.sol file which contains the contract(s) code and all its dependencies, which we will copy and paste to the etherscan when verifying the contract.

- Make sure in your `flattened.sol` file, `// SPDX-License-Identifier: MIT` is only mentioned one time. Otherwise, it will throw you an error.

### Step 8: Verifying the Contract on Sepolia Testnet

# Enjoy your day.