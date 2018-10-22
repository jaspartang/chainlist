# Udemy Blockchain Course - Manual Contact Deployment

The code in this directory and sub-directories were build following the
[Udemy Blockchain]()
course.

The code in the directory was created by the following command.

- `truffle unbox chainskills/chainskills-box`

# Process

- start Ganache GUI
- start Metamask
  - import the Ganache account, if not already imported, and name them
  - connect Metamask to the Ganache network
- wrote `ChainList.sol` contract
- wrote `2_deploy_contracts` contract
- `truffle migrate --network ganache` deployed the contract to Ganache
- `truffle console --network ganache` for the repl to use following commands
  - `ChainList.address` for Chainlist address
  - `web3.fromWei(web3.eth.getBalance(web3.eth.accounts[0]), "ether").toNumber()`
    - check account balance
  - `ChainList.deployed().then(function(instance) {app = instance;});`
    - get instance of contract
  - `app.sellArticle('shirt','covers your back', web3.toWei(1,"ether"),{from: web3.eth.accounts[1]})`
    - sell an article
  - `app.getArticle()`
    - get an article information
- `truffle test` to test after writing `ChainListHappyPath.js` mocha/chai test
- `truffle migrate --compile-all --reset --network ganache` deployed the contract to Ganache
- add event to contract
- `sellEvent = app.LogSellArticle({},{fromBlock: 0, toBlock: 'latest'}).watch((err, event)=> console.log(event))`
  - at truffle console watch contract event after gettging app instance
- sell an article and watch an event fire
- `sellEvent.stopWatching()` - to stop watching events