# Udemy Blockchain Course - Manual Contact Deployment

The code in this directory and sub-directories were build following the
[Udemy Blockchain]()
course.

The code in the directory was created by the following command.

- `truffle unbox chainskills/chainskills-box`

The distributed frontend can be accessed
[here](https://carltonj2000.github.io/chainlist/).

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
- `web3.personal.unlockAccount(web3.eth.accounts[1],"pass1234",600);`
  - when connecting to a private geth instance have to unlock and account to
    use it. the seconds parameter is the number of seconds to keep the account
    unlocked.
  - `from: "<account address>"`
    - The above line is needed in the truffle.js file for the selected network
      in order to deploy contracts from the an account other than the
      coninbase/accounts[0]
- `buyEvent = app.LogBuyArticle({_seller: web3.eth.accounts[1]},{}).watch((er, event)=> console.log(event))`
  - at truffle console watch a contract event after gettging app instance
- `App.buyArticle({from: web3.eth.accounts[2], value: web3.toWei(10, "ether")})`
  - buy the article
- `debug "<tx hash>"` - at truffle prompt debug a transaction
- https://ethgasstation.info/ - to use when setting your gas price for contracts

## Commands In Order Of Usual Execution

- truffle console --network ganache
- truffle migrate --compile-all --reset --network ganache
- ChainList.deployed().then(function(instance) {app = instance;})
- sellEvent = app.LogSellArticle({},{}).watch((err, event)=> console.log(event))
- app.getNumberOfArticles();
- app.getArticlesForSale();
- app.sellArticle('Article 1','Description of Article 1', web3.toWei(3,"ether"),{from: web3.eth.accounts[1]})
- app.sellArticle('Article 2','Description of Article 2', web3.toWei(3,"ether"),{from: web3.eth.accounts[2]})
- app.sellArticle('Article 3','Description of Article 3', web3.toWei(3,"ether"),{from: web3.eth.accounts[1]})
- app.articles(1)
- app.buyArticle(1,{from: web3.eth.accounts[3], value: web3.toWei(3,"ether")})

# Rinkeby

- geth --rinkeby account new - create 3 new accounts
- geth --rinkeby --datadir /home/carltonmac/cj/cj2018mac/ethereum/rinkebychain
- geth --rinkeby --datadir /home/carltonmac/cj/cj2018mac/ethereum/rinkebychain account new
- use the startrinkeby-linux/mac.sh to run the script
- can access geth remotely by the setting up a tunnl
  - ssh -f -N -L 8545:localhost:8545 carltonmac@10.0.0.137
  - keep the ssh connection alive in ~/.ssh/config

```
Host *10.0.0.137
  ServerAliveInterval 60
```

- geth attach
  - eth.syncing - returns false if complete, otherwise present status numbers
  - personal.unlockAccount(eth.accounts[0],"password",1200);
- truffle migrate --compile-all --reset --network rinkeby
- https://rinkeby.etherscan.io - use to check your transactions

# Linux Setup

sudo apt install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt update
sudo apt install ethereum
goto truffleframework.com and download ganache, chmod +x, run to install
install node
npm install truffle -g

# MAC Setup

brew ??
install node
goto truffleframework.com and download ganache, run to install
