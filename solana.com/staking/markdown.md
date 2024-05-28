This website uses cookies to offer you a better browsing experience. Find out
more on how we use cookies.

Opt-out[Details](/privacy-policy#collection-of-information)

Accept

[![Solana](/_next/static/media/logotype.e4df684f.svg)](/)

  * Learn
  * Developers
  * Solutions
  * Network
  * Community

Search```K`

# Staking and Inflation FAQ

### Overview

  * Through an on-chain governance process, Solana's community of validators voted to enable staking rewards and inflation, which are now live.
  * SOL token holders can earn rewards and help secure the network by staking tokens to one or more [validators on Solana’s Mainnet Beta](https://solanabeach.io/validators) .
  * Returns/yield for staked tokens is based on the current inflation rate, total number of SOL staked on the network, and an individual validator’s uptime and commission (fee).
  * Solana's initial inflation rate is 8% annually, decreasing by 15% year-over-year, reaching a long-term fixed inflation rate of 1.5% annually.

## Staking Overview

What is Proof-of-Stake?

On the Solana network, many different people andentities run a program on
specialized computers known asa validator. Validators play a key role in
maintainingand securing the Solana blockchain. Validators areresponsible for
processing new incoming transactions onthe network, as well as for voting on
and appending newblocks to the blockchain.

As different validators around the world may receivedifferent pieces of
information at different times, itis essential that the network is able to
come toagreement about which transactions and data arecontinually added to the
blockchain. The strategy bywhich the validators and the entire network come to
thisagreement is known as the consensus mechanism, and is acore challenge to
building a successful decentralizedblockchain network. Many different projects
haveattempted various solutions on how to reach consensus ina fast and cost-
efficient manner.

The Solana network uses a Proof-of-Stake consensusmechanism (often abbreviated
to PoS). Every validator onthe network has an opportunity to participate
inconsensus by casting votes for which blocks they believeshould be added to
the blockchain, thereby confirmingany valid transactions contained in those
particularblocks. However, not all validator’s votes are weightedequally.

Validator’s consensus votes are stake-weighted, meaningthe more stake an
individual validator has, the moreinfluence that one validator has in
determining theoutcome of the consensus voting. Similarly, validatorswith less
stake have less weight in determining the voteoutcome, and validators with no
stake cannot influencethe outcome of a consensus vote.

What is staking?

Staking is the process by which a SOL token holder (such as someone who
purchased SOL tokens on an exchange) assigns some or all of their tokens to a
particular validator or validators, which helps increase those validators’
voting weight. Assigning your tokens to add to a validator’s stake-weight is
known as “delegating” your tokens. Delegating your tokens to a validator does
NOT give the validator ownership or control over your tokens. At all times,
you still control all your staked tokens that you may have chosen to delegate.

By staking tokens with a validator or validators, the token holder indicates a
degree of trust in the validator they chose to delegate to. As validators
amass larger amounts of stake delegations from different token holders, this
acts as “proof” to the network that the validator’s consensus votes are
trustworthy, and their votes are therefore weighted proportionally to the
amount of stake the validator has attracted. By weighing the collective votes
from all validators against the proportion of stake that has been delegated to
them, the network reaches consensus by this Proof of Stake.

As different validators around the world may receivedifferent pieces of
information at different times, itis essential that the network is able to
come toagreement about which transactions and data arecontinually added to the
blockchain. The strategy bywhich the validators and the entire network come to
thisagreement is known as the consensus mechanism, and is acore challenge to
building a successful decentralizedblockchain network. Many different projects
haveattempted various solutions on how to reach consensus ina fast and cost-
efficient manner.

The Solana network uses a Proof-of-Stake consensusmechanism (often abbreviated
to PoS). Every validator onthe network has an opportunity to participate
inconsensus by casting votes for which blocks they believeshould be added to
the blockchain, thereby confirmingany valid transactions contained in those
particularblocks. However, not all validator’s votes are weightedequally.

Validator’s consensus votes are stake-weighted, meaningthe more stake an
individual validator has, the moreinfluence that one validator has in
determining theoutcome of the consensus voting. Similarly, validatorswith less
stake have less weight in determining the voteoutcome, and validators with no
stake cannot influencethe outcome of a consensus vote.

Why stake?

In an open and decentralized network like Solana, anyone can run a validator
if they choose. A malicious validator or other bad actor could attempt to
attack the network or to submit incorrect or fraudulent transactions for their
own gain. Because of the Proof-of-Stake consensus mechanism described above, a
single entity acting alone in this fraudulent manner would need to attract
some amount of stake before any of their proposed activities would be weighed
in the consensus vote. As more token holders choose to stake their SOL tokens
to different validators across the network, and the total amount of stake on
the network increases, it becomes increasingly difficult for even a
coordinated and well-funded attacker to amass enough stake to single-handedly
alter the outcome of a consensus vote for their own benefit. In short, the
more stake that is delegated to many different validators across the network,
the more safe and secure the network becomes for all of its users.
Additionally, token holders who choose to stake their tokens and help secure
the network in doing so, are eligible to receive staking rewards once they
have delegated their tokens to one or more validators. More details on staking
rewards are found below.

Are there risks associated with staking?

On many Proof-of-Stake networks, there exists a mechanism known as “slashing”.
Slashing is any process by which some portion of stake delegated to a
validator is destroyed as a punitive measure for malicious actions undertaken
by the validator.

This mechanism incentivizes validators not to undertake such actions, as less
stake delegated to a validator means that validator then accrues fewer
rewards. Being slashed can also be seen as a reputational risk for retaining
current or attracting potential future stake.

Slashing also poses a risk to token holders who could potentially lose some of
their tokens if they have delegated to a validator which gets slashed. The
presence of slashing could incentivize token holders to only delegate their
tokens to validators they feel are reputable, and not to delegate all their
tokens to a single or small number of validators.

On Solana, slashing is not automatic. If an attacker causes the network to
halt, they can be slashed upon network restart. For more information, please
check out [the Solana Validator
docs.](https://docs.solanalabs.com/proposals/optimistic-confirmation-and-
slashing#slashing-roadmap)

Who can stake?

Anyone who holds SOL can stake their tokens at any time.

How do I stake my tokens?

To stake SOL tokens, you must use a wallet that supports staking. Not all
wallets support staking at this time. SolFlare.com is one user-friendly wallet
that supports staking. Check out the official docs for [a list of wallets
which support staking.](https://solana.com/docs/economics/staking#supported-
wallets)

SOL tokens in your wallet must first be moved into a stake account. You can
create as many stake accounts as you like, and deposit as much or as little
SOL into each stake account as you want. Each new stake account has a unique
address, and a single wallet can manage or “authorize” many different stake
accounts. Check out our docs on [stake account
structure](https://solana.com/docs/economics/staking/stake-accounts) for more
details.

In order to earn staking rewards (if inflation is enabled on Mainnet Beta),
the tokens in a stake account must be delegated to a validator. A single stake
account can only be delegated to a single validator at any time, so if you
want to delegate to different validators you will need to split your tokens
between multiple stake accounts.

  

Where can I learn about the validators on Solana?

There are various community-operated tools where you can view information
about the network as well as certain performance metrics about individual
validators, such as:

  * [Solanabeach.io](https://solanabeach.io/)
  * [Validators.app](https://validators.app/)

Many validators also chose to introduce themselves and their services on the
Solana forums:

  * <https://forums.solana.com/t/validator-information-thread/577>

Can I stake tokens from an account if my tokens have a lockup?

Yes. Some people may have received a stake account with locked up tokens from
the Solana Foundation that was distributed in exchange for services. Tokens in
stake accounts with a lockup may not be withdrawn to another wallet address
before the lockup expires, but they may still be delegated to a validator to
potentially earn staking rewards during this time. Rewards earned on locked
tokens are deposited back into the locked stake account.

How do I add tokens to a stake account?

When you first create a stake account, you specify how many SOL tokens you
want to fund it with, and these tokens are withdrawn from your main wallet
account and deposited into the new stake account.

Tokens can also be transferred into a pre-existing stake account at any time,
by using your wallet’s Transfer or Send feature and providing the address of
your stake account. If you transfer tokens into a stake account that is
already delegated, these new tokens will not automatically be delegated.

If you have a delegated stake account and you wish to increase your delegation
to a particular validator, the best practice is to create a new stake account
with the additional amount of stake and delegate that account to the same
validator.

Example: Increasing the stake delegated to a single validator

  * User has a wallet with 1000 SOL balance.
  * User uses the wallet interface to create a stake account with 100 SOL, then delegates the tokens in the stake account to Validator A.
  * Wallet balance is now 900 SOL and the wallet also controls a stake account with a balance of 100 SOL.
  * The stake account shows in the wallet interface and on the Explorer that it is “Activating”. Once it is “Active”, the staked tokens are eligible for rewards. See [Timing Considerations](https://solana.com/staking/#overview/delegation-timing-considerations) for more details.
  * Later, the user wants to increase their delegation to Validator A, so uses the wallet interface to create a second stake account with 50 SOL, then delegates the tokens in the new stake account to Validator A.
  * Wallet balance is now 850 SOL and the wallet also controls 2 stake accounts with 100 and 50 SOL, respectively, each delegated to Validator A.

If you transfer tokens into a stake account that is already delegated, these
new tokens will not automatically be delegated. In order to get these new
tokens also delegated and earning rewards, you would need to un-delegate the
entire account, then re-delegate the same account. As un-delegating and re-
delegating [can take several days to take
effect](https://solana.com/staking/#overview/delegation-timing-
considerations), your original stake would not be earning rewards during this
transition period.

Therefore, we recommend only transferring SOL into a stake account when it is
first created or otherwise not delegated.

How do I remove tokens from an existing stake account?

Tokens can only be withdrawn from a stake account when they are not currently
delegated. When a stake account is first un-delegated, it is considered
“deactivating” or “cooling down”. Tokens may not be withdrawn from the account
until some or all of them have finished deactivating and are considered
“inactive” and therefore no longer earning any potential staking rewards. For
details on how long this transition period may take, please see [Timing
Considerations](https://solana.com/staking/#overview/delegation-timing-
considerations).

Once the tokens in a stake account are inactive, they can be withdrawn back to
your main wallet address or to another address immediately.

Example: Withdrawing all tokens from a stake account

  * User has a wallet with a balance of 900 SOL, and a single stake account with 100 SOL delegated to a validator.
  * User uses the wallet interface to Deactivate their stake delegation. The stake account shows in the wallet interface and on the Explorer that it is “Deactivating”. Once it is “Inactive” or “Not Delegated”, the staked tokens stop earning rewards and can be withdrawn. See [Timing Considerations](https://solana.com/staking/#overview/delegation-timing-considerations) for more details.
  * User can use the wallet interface to withdraw their all tokens back into their main wallet account. The wallet balance now shows 1,000 SOL and the stake account is closed.

If you want to reduce the amount of delegated stake assigned to a given
validator without deactivating your entire balance (and therefore missing any
potential rewards during the delegation downtime), you can Split an existing
stake account into two accounts, and undelegate one, while leaving the other
account delegated and continuously eligible for rewards.

Example: Reducing the delegation staked to a given validator

  * User has a wallet with a balance of 800 SOL, and a single stake account with 200 SOL delegated to a validator.
  * User wants to reduce the amount of stake delegated to the validator by 100 SOL.
  * Use the wallet interface to “Split” the stake account, and specifies 100 SOL as the amount to split.
  * There are now 2 stake accounts, each with 100 SOL which are each delegated to the same validator.
  * User can then use the wallet interface to Deactivate one of their stake delegations. The stake account shows in the wallet interface and on the Explorer that it is “Deactivating”. Once it is “Inactive” or “Not Delegated”, the staked tokens stop earning rewards and can be withdrawn. See [Timing Considerations](https://solana.com/staking/#overview/delegation-timing-considerations) for more details.
  * Once the account is Inactive, the user can then choose to delegate the account to a different validator, or to withdraw the tokens back into the main wallet, or to further split the inactive stake account and delegate to multiple different validators.

Tokens in a stake account with a lockup may not be withdrawn until the lockup
expires, regardless of the delegation state of that account. Once the lockup
expires, undelegated tokens may be withdrawn immediately. There is no action
required by the account holder to specifically unlock the account.

  

Delegation Timing Considerations

When you delegate or un-delegate a stake account, the tokens do not change
state immediately. Newly delegated tokens are considered “activating” or
“warming up”, and are not eligible to earn rewards until they are fully
activated. Newly un-delegated tokens are considered “deactivating” or “cooling
down” and are not able to be withdrawn until deactivated.

The Solana protocol only allows stake tokens to finish changing state at the
beginning of a new epoch. An epoch is approximately 2 days long. Use `solana
epoch-info` to see details of the current epoch.

If you delegate tokens in a stake account in the middle of an epoch, the
tokens will appear in your wallet as “activating” until the current epoch
ends, at which point they will be active and eligible to earn rewards. Whether
you delegate your stake tokens near the beginning of the current epoch, or
near the end of the current epoch does not impact when the tokens will become
active, which is only at the next epoch boundary. The same logic applies to
un-delegating or deactivating a delegated stake account. Deactivating tokens
cannot be withdrawn until they have finished deactivating at the epoch
boundary.

There is a limit to how much total stake can change state in a single epoch
across the entire Solana network. No more than 25% of the total active stake
on the network can be activated or deactivated in a single epoch. In a
scenario where more than 25% of the total active take on the network is being
activated in a single epoch, a portion of all activating/deactivating stake up
to the global 25% limit, will finish changing state at the first epoch
boundary. The remaining stake would stay as “activating” or “deactivating” for
at least one more epoch, until the next epoch boundary.

If a stake activation takes multiple epochs, the portion of stake that becomes
fully active at the first epoch boundary is eligible for rewards, while the
remaining portion that is still activating for an additional epoch is not yet
eligible for rewards.

Similarly, if a stake deactivation takes multiple epochs, the portion of stake
that becomes fully inactive at the first epoch boundary becomes able to be
withdrawn, while the remaining portion is still deactivating for an additional
epoch, at which point it can then be withdrawn.

  

How can I check on the status of a specific stake account?

All stake accounts on Solana (and all accounts of any variety) can be viewed
on Solana’s network explorer, found here:

[**Solana Explorer**](https://explorer.solana.com)

Copy and paste the stake account address of interest in the main search bar of
the explorer to see details of the account, including its
activation/deactivation/delegation status, current balance, and the address of
the stake account’s authorities, which would usually be the same as your
wallet’s main address.

Depending on which wallet solution you use to manage your stake accounts, this
same information may be visible by logging in to your wallet and viewing your
stake accounts.

## Staking Rewards

How do I estimate and view my staking rewards?

Staking rewards are computed and issued once per epoch. An epoch is
approximately 2 days long. Rewards accrued in a given epoch are issued to all
validators and delegators in the first block of the following epoch. Staking
yield is presented as an annualized figure, though this number varies each
epoch as the inflation rate and total active stake continually change. Staking
yield and the full inflation design is detailed in our official docs
[here.](https://solana.com/docs/economics/inflation/terminology)

![](/src/img/staking/validator1.png)

Estimates of Staking Yield, given various models of the fraction of total SOL
staked, can be explored here:

[**STAKING YIELD MODELS**](https://solana.shinyapps.io/inflation-proposal/)

To estimate the amount of SOL a delegator can expect to see in a single epoch
in a single stake account:

![](/src/img/staking/validator3.png)

What is Validator Uptime?

Validator Uptime is defined by a validator’s consensus voting behavior. For
each time a validator votes on a block that is ultimately appended to the
blockchain, that validator earns one Vote Credit.

When rewards are tallied at the end of the epoch, all the stake-weighted vote
credits earned by all the validators are used to determine the total amount of
SOL that is issued to each particular validator and their delegators.

  

What is the Validator Fee/Commission?

Validators charge a fee on inflationary rewards earned by the stake accounts
that are delegated to them, in exchange for their services in securing the
blockchain and processing transactions. This fee is known as the commission
rate. Each time rewards are issued, the commission is deposited in the
validator’s account and the remaining rewards are deposited in all of the
stake accounts that are delegated to that validator, proportionally to the
amount of actively delegated stake in each account. Validator commission and
staking rewards are always issued simultaneously.

When and where are staking rewards issued?

Rewards are issued once per epoch and are deposited into the stake account
that earned them. Stake rewards are automatically re-delegated as active
stake.

If the rewards due to a validator or one of their stakes is less than one
lamport for a given epoch, reward issuance is deferred until the next epoch in
which both would receive at least one lamport.

## Economics

What will the inflation rate be?

The details of the originally proposed inflation schedule are discussed here.
The specific parameters that determine the inflation schedule are:

  1. Initial Inflation Rate: 8 %
  2. Dis-inflation Rate: −15%
  3. Long-term Inflation Rate: 1.5%

The above parameters are defined as:

  * Initial Inflation Rate: The starting Inflation Rate for when inflation is first enabled. The token issuance rate can only decrease from this amount
  * Dis-inflation Rate: The annualized rate at which the Inflation Rate is reduced
  * Long-term Inflation Rate: The stable, long-term Inflation Rate to be expected

Note that the inflation rate will not be the same as the staking yield (i.e.
the interest earned by staking tokens). See below for a discussion of staking
yield.

  

Where will the inflationary issuance be distributed?

100% of the inflationary issuances are proposed to be delivered to delegated
stake accounts and validators.

What is the expected staking yield?

Staking yield comes from inflationary issuances being distributed across
delegated staking accounts and validator vote accounts per the validator
commission rate. Due to this design, the staking yield is to be primarily a
function of the fraction of SOL that is staked on the network. A detailed
discussion of the design and its impact on staking yield can be found here:

[**INFLATION DESIGN OVERVIEW**](https://forums.solana.com/t/solana-inflation-
design-overview/920)

The amount of total SOL that will be staked is unknown, so we can only
estimate the exact staking yields. Below, we show staking yields over time
segmented by different values of the percent of staked SOL that might be
observed on the network (between 60-90%). The inflation schedule parameters
are set as described above.

![](/src/img/staking/validator2.png)

A simple interactive dashboard is provided here, in which different % of
staked SOL can be selected to see the impact on prospective staking yields.

Please note that this is an idealized Staked Yield as it neglects validator
uptime impact on rewards, validator commissions, potential yield throttling
and potential slashing incidents. It additionally ignores that % of Staked SOL
is dynamic by design, i.e. it is expected that the % of staked SOL changes
over time thus impacting the staking yield over time. It is only presented to
be used as a rough estimate for expected staking yields.

![](https://cdn.builder.io/api/v1/pixel?apiKey=ce0c7323a97a4d91bd0baa7490ec9139)

Managed by

[](/)

[](/youtube)[](/twitter)[](/discord)[](/reddit)[](/github)[](/telegram)

© 2024 Solana Foundation. All rights reserved.

Solana

  * [Grants](https://solana.org/grants)
  * [Break Solana](https://break.solana.com/)
  * [Media Kit](/branding)
  * [Careers](https://jobs.solana.com/)
  * [Disclaimer](/tos)
  * [Privacy Policy](/privacy-policy)

Get Connected

  * [Ecosystem](/ecosystem)
  * [Blog](/news)
  * [Newsletter](/newsletter)

en

© 2024 Solana Foundation. All rights reserved.

