# Express-Web3-API

A simple example of locally exposing API endpoints using Express that read data from Smart Contracts deployed on a local blockchain test network.

## Getting Started

Clone the Repo from Git


Start Ganache from Blockchain-Dev directory (may have to run yarn install first, please let me know)
```
node_modules/.bin/ganache-cli
```

In Another Terminal run Node Console
```
node
```

Deploy our example Smart Contract, Voting.sol in Node Console
```
> Web3 = require('web3')
> web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
> web3.eth.accounts
> code = fs.readFileSync('Voting.sol').toString()
> solc = require('solc')
> compiledCode = solc.compile(code)
> abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
> VotingContract = web3.eth.contract(abiDefinition)
> byteCode = compiledCode.contracts[':Voting'].bytecode
> deployedContract = VotingContract.new(['Rama','Nick','Jose'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
```

IMPORTANT! - Retrieve contract's address and save
```
> deployedContract.address 
> contractInstance = VotingContract.at(deployedContract.address)
```

In Another Terminal edit server.js and change the address to the address you just saved
```
const contractInstance = VotingContract.at('YOUR_ADDRESS_HERE');
```

And again in index.js ...
```
contractInstance = VotingContract.at('YOUR_ADDRESS_HERE');
```

Start server from Blockchain-Dev directory
```

yarn server
```

and test it works by navigating to http://localhost:5000/api/hello

Navigate to http://localhost:5000/api/votes/Rama to validate the API returns 0 votes.

In another Terminal open the index.html to see a simple UI
```
open index.html
```

In this UI you can add votes to the candidates.  Try 'Rama' and click Vote button.
Go back to the http://localhost:5000/api/votes/Rama endpoint to confirm change.


### TODO:

* Update Readme with Prereqs, installation steps, running tests, etc
* Replace Voting.Sol with a generic smart contract
* Update smart contract deploy process to Truffle
* Possibly update Express server to Webpack
* Authentication
* Deploy and connect on testnet rather than Ganache (make this a configurable environment variable)

### Dev Notes:

* Need to check if UI code can hit the server (may need to provide proxy)



## Resources

* https://medium.freecodecamp.org/how-to-make-create-react-app-work-with-a-node-backend-api-7c5c48acb1b0
* https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2

