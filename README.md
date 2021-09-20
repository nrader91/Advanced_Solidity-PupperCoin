# Advanced_Solidity-PupperCoin
Advanced implementation of smart contract within a real world example. 

## Intro
Your compnay has decided to crowdsale their own token "PupperCoin" in order to fund the companies network development. This network will be used to track the dog breeding activity across the globe in a decentralized way, and allow humans to track the genetic trail of their pets. You have already worked with the necessary legal bodies and have the green light on creating a crowdsale open to the public. However, you are required to enable refunds if the crowdsale is successful and the goal is met, and you are only allowed to raise a maximum of 300 Ether. The crowdsale will run for 24 weeks.

You will need to create an ERC20 token that will be minted through a Crowdsale contract that you can leverage from the OpenZeppelin Solidity library.

This crowdsale contract will manage the entire process, allowing users to send ETH and get back PUP (PupperCoin).
This contract will mint the tokens automatically and distribute them to buyers in one transaction.

## Instructions 

1) Create a new contract on Remix.

2) ERC20 PupperCoin - You will need to simply use a standard ERC20Mintable and ERC20Detailed contract, hardcoding 18 as the decimals parameter, and leaving the initial_supply parameter alone.

3) Since RefundablePostDeliveryCrowdsale inherits the RefundableCrowdsale contract, which requires a goal parameter, you must call the RefundableCrowdsale constructor from your PupperCoinCrowdsale constructor as well as the others. RefundablePostDeliveryCrowdsale does not have its own constructor, so just use the RefundableCrowdsale constructor that it inherits.

If you forget to call the RefundableCrowdsale constructor, the RefundablePostDeliveryCrowdsale will fail since it relies on it (it inherits from RefundableCrowdsale), and does not have its own constructor.

When passing the open and close times, use now and now + 24 weeks to set the times properly from your PupperCoinCrowdsaleDeployer contract.

## Testing
Test the crowdsale by sending Ether to the crowdsale from a different account (not the same account that is raising funds), then once you confirm that the crowdsale works as expected, try to add the token to MyCrypto and test a transaction. You can test the time functionality by replacing now with fakenow, and creating a setter function to modify fakenow to whatever time you want to simulate. You can also set the close time to be now + 5 minutes, or whatever timeline you'd like to test for a shorter crowdsale.

When sending Ether to the contract, make sure you hit your goal that you set, and finalize the sale using the Crowdsale's finalize function. In order to finalize, isOpen must return false (isOpen comes from TimedCrowdsale which checks to see if the close time has passed yet). Since the goal is 300 Ether, you may need to send from multiple accounts. If you run out of prefunded accounts in Ganache, you can create a new workspace.
Remember, the refund feature of 

RefundablePostDeliveryCrowdsale only allows for refunds once the crowdsale is closed and the goal is met. See the OpenZeppelin RefundableCrowdsale documentation for details as to why this is logic is used to prevent potential attacks on your token's value.

## Deployment
Deploy the crowdsale to the Kovan or Ropsten testnet, and store the deployed address for later. Switch MetaMask to your desired network, and use the Deploy tab in Remix to deploy your contracts. Take note of the total gas cost, and compare it to how costly it would be in reality. Since you are deploying to a network that you don't have control over, faucets will not likely give out 300 test Ether. You can simply reduce the goal when deploying to a testnet to an amount much smaller, like 10,000 wei.
