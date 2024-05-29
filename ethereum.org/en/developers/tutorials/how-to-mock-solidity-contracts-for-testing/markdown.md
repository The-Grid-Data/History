Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# How to mock Solidity smart contracts for testing

soliditysmart contractstestingmocking

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Markus
Waas

![📚](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4da.svg)[soliditydeveloper.com(opens
in a new tab)](https://soliditydeveloper.com/mocking-contracts)

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
May 2, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * Unit-testing contracts with mocks
  * Example: Private ERC20
  * Mocking many contracts
  * Mocking can be even more powerful

[Mock objects(opens in a new tab)](https://wikipedia.org/wiki/Mock_object) are
a common design pattern in object-oriented programming. Coming from the old
French word 'mocquer' with the meaning of 'making fun of', it evolved to
'imitating something real' which is actually what we are doing in programming.
Please only make fun of your smart contracts if you want to, but mock them
whenever you can. It makes your life easier.

## Unit-testing contracts with mocks

Mocking a contract essentially means creating a second version of that
contract which behaves very similar to the original one, but in a way that can
be easily controlled by the developer. You often end up with complex contracts
where you only want to [unit-test small parts of the
contract](/en/developers/docs/smart-contracts/testing/). The problem is what
if testing this small part requires a very specific contract state that is
difficult to end up in?

You could write complex test setup logic every time that brings in the
contract in the required state or you write a mock. Mocking a contract is easy
with inheritance. Simply create a second mock contract that inherits from the
original one. Now you can override functions to your mock. Let us see it with
an example.

## Example: Private ERC20

We use an example ERC-20 contract that has an initial private time. The owner
can manage private users and only those will be allowed to receive tokens at
the beginning. Once a certain time has passed, everyone will be allowed to use
the tokens. If you are curious, we are using the [`_beforeTokenTransfer`(opens
in a new tab)](https://docs.openzeppelin.com/contracts/3.x/extending-
contracts#using-hooks) hook from the new OpenZeppelin contracts v3.

    
    
    1pragma solidity ^0.6.0;
    
    2
    
    3import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
    
    4import "@openzeppelin/contracts/access/Ownable.sol";
    
    5
    
    6contract PrivateERC20 is ERC20, Ownable {
    
    7    mapping (address => bool) public isPrivateUser;
    
    8    uint256 private publicAfterTime;
    
    9
    
    10    constructor(uint256 privateERC20timeInSec) ERC20("PrivateERC20", "PRIV") public {
    
    11        publicAfterTime = now + privateERC20timeInSec;
    
    12    }
    
    13
    
    14    function addUser(address user) external onlyOwner {
    
    15        isPrivateUser[user] = true;
    
    16    }
    
    17
    
    18    function isPublic() public view returns (bool) {
    
    19        return now >= publicAfterTime;
    
    20    }
    
    21
    
    22    function _beforeTokenTransfer(address from, address to, uint256 amount) internal virtual override {
    
    23        super._beforeTokenTransfer(from, to, amount);
    
    24
    
    25        require(_validRecipient(to), "PrivateERC20: invalid recipient");
    
    26    }
    
    27
    
    28    function _validRecipient(address to) private view returns (bool) {
    
    29        if (isPublic()) {
    
    30            return true;
    
    31        }
    
    32
    
    33        return isPrivateUser[to];
    
    34    }
    
    35}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

And now let's mock it.

    
    
    1pragma solidity ^0.6.0;
    
    2import "../PrivateERC20.sol";
    
    3
    
    4contract PrivateERC20Mock is PrivateERC20 {
    
    5    bool isPublicConfig;
    
    6
    
    7    constructor() public PrivateERC20(0) {}
    
    8
    
    9    function setIsPublic(bool isPublic) external {
    
    10        isPublicConfig = isPublic;
    
    11    }
    
    12
    
    13    function isPublic() public view returns (bool) {
    
    14        return isPublicConfig;
    
    15    }
    
    16}
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

You will get one of the following error messages:

  * `PrivateERC20Mock.sol: TypeError: Overriding function is missing "override" specifier.`
  * `PrivateERC20.sol: TypeError: Trying to override non-virtual function. Did you forget to add "virtual"?.`

Since we are using the new 0.6 Solidity version, we have to add the `virtual`
keyword for functions that can be overridden and override for the overriding
function. So let us add those to both `isPublic` functions.

Now in your unit tests, you can use `PrivateERC20Mock` instead. When you want
to test the behavior during the private usage time, use `setIsPublic(false)`
and likewise `setIsPublic(true)` for testing the public usage time. Of course
in our example, we could just use [time helpers(opens in a new
tab)](https://docs.openzeppelin.com/test-helpers/0.5/api#increase) to change
the times accordingly as well. But the idea of mocking should be clear now and
you can imagine scenarios where it is not as easy as simply advancing the
time.

## Mocking many contracts

It can become messy if you have to create another contract for every single
mock. If this bothers you, you can take a look at the [MockContract(opens in a
new tab)](https://github.com/gnosis/mock-contract) library. It allows you to
override and change behaviors of contracts on-the-fly. However, it works only
for mocking calls to another contract, so it would not work for our example.

## Mocking can be even more powerful

The powers of mocking do not end there.

  * Adding functions: Not only overriding a specific function is useful, but also just adding additional functions. A good example for tokens is just having an additional `mint` function to allow any user to get new tokens for free.
  * Usage in testnets: When you deploy and test your contracts on testnets together with your dapp, consider using a mocked version. Avoid overriding functions unless you really have to. You want to test the real logic after all. But adding for example a reset function can be useful that simply resets the contract state to the beginning, no new deployment required. Obviously you would not want to have that in a Mainnet contract.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/how-to-mock-solidity-contracts-for-testing/index.md)
  * On this page

    * Unit-testing contracts with mocks
    * Example: Private ERC20
    * Mocking many contracts
    * Mocking can be even more powerful

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

