s m a r t

w a l l e t s

a t

l i g h t s p e e d

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[About](https://www.sqds.io/)

[Blog](../blog)

[](../)

Get started

# Solana Validator Management with Multisig

May 22, 2023

![solana-validator-withdraw-key-stake-pool-manager-withdrawer-keypair-
management-validator-multisig-vote-account-stake-account-hardware-wallets-for-
validators-
multisig](https://framerusercontent.com/images/U8UTf8cORN4ve0phO11BY6aGJk.png)

Multisig solutions have finally started to be considered not only for treasury
management, as they are also becoming a standard for managing program
authorities of protocols. But another significant use case of multisig is
validator management. Whether for individual validators or stake pool
managers, a multi-signature wallet is a great alternative to traditional self-
custody solutions like hardware wallets to secure their operations.

This article aims to introduce management of Solana validators and stake pools
with multisig and its benefits compared to current solutions. Although it is
often more suitable for teams and organizations, we'll also cover how
validators managed by a single operator can use Squads in their setup.

## Multisig and Individual Validator Management

Multisig, short for multi-signature, is a self-custody solution using a
mechanism where multiple signatures are required to execute a transaction.
Upon creation, several owners (private keys) are added, and a signature
threshold is set. The multisig can then be used to store and manage any on-
chain asset that a regular key can control, such as treasury assets or
authority keys of programs, tokens, or validators. Any action involving the
assets held within the multisig requires approval from the owners and must
meet the set signature threshold.  
  

![squads-multisig-solana-wallet-validator-withdraw-key-management-solana-
immutable-multisig-how-it-
works](https://framerusercontent.com/images/dMyb3W22ShkG8rvq5tQawdl3WMw.webp)

This setup is perfectly suited for teams and organizations that need to
distribute control over on-chain assets among multiple stakeholders. Multisig
ensures that no single point of failure exists - even if one person or private
key gets compromised, the assets remain secure. This is because several keys
are added as owners to the multisig. Thus, it becomes more challenging for
unauthorized actions to occur as each owner has visibility over every
transaction and must approve them.

On Solana, individual validators primarily manage two authority keys: the vote
authority, and the withdraw authority. Authority keys grant total control over
on-chain assets and can update them. Programs, tokens, validators, and more
have authority keys to manage specific types of operations. While the
validator vote authority is used solely for voting, the withdraw authority
serves as a sort of master authority key and requires the highest security
measures to prevent undesired situations. It has the power to change the
validator identity as well as the authorized voter, adjust the commission
rate, or withdraw rewards. The core business of a validator depends on it - if
something happens to this key, it could severely damage the validator's
operations.  
  

![solana-validator-withdraw-authority-key-vote-account-vote-authority-
withdrawer-keypair-validator-management-
multisig](https://framerusercontent.com/images/Y37BimL2HvVqPPdSPFiNykUX5X8.png)

Using a simple hot/cold wallet solution or a CLI wallet to manage authority
keys is potentially risky for teams and organizations, primarily because:

  * One person holds all decision-making power;

  * These wallet solutions can be easily compromised.

In such scenarios, a multisig is likely the best option. By delegating the
withdraw authority key to it, a validator can split the ownership among
various owners/private keys, each having a decision-making power to execute
transactions involving the validator key. This can include actions like
changing the commission rate or rotating the vote account authority keys.
Additionally, it eliminates a single point of failure - even if one key of the
multisig is compromised, it cannot use or affect the withdraw authority.

Squads has built a platform that facilitates the creation of a multisig and
management of various types of on-chain assets, including validator withdraw
authorities. Operators can transfer their validator key using their CLI, and
then manage the commission rate and withdraw rewards directly from the
interface. Additionally, the Squads multisig program is open-source and
[immutable](https://twitter.com/SquadsProtocol/status/1628776620243963904)
(non-upgradeable), which means that no one besides you can access or move your
withdraw authority key.  
  

![squads-multisig-wallet-solana-validator-withdraw-authority-key-multi-
signature-immutable-non-upgreadable-open-source-audited-
multisig](https://framerusercontent.com/images/YyyiXNnYSnHav1RJCAeSKG0rQ.png)

On top of this, this setup streamlines the operation of validators. Since the
key is held within the multisig, the validator operators can easily withdraw
the rewards to their Squad and manage them collectively (e.g. to cover
expenses such as salaries). Simply put, the Squads multi-signature
functionality provides the same benefits for managing treasury assets, such as
validator revenues, as it does for the withdraw authority. This makes it a
secure and efficient management solution for all business aspects of a
validator.

## Stake Pool Management with Multisig

Solana stake pools, another type of staking ecosystem stakeholder, can also
greatly benefit from a multisig setup. These pools are a collection of one or
more validator nodes that enable delegators to stake to multiple validators at
once, often promoting better decentralization and mitigating the risks
associated with unexpected validator node downtime. Stake pool managers on
Solana, such as Jito, Marinade, Cogent, Laine, SolBlaze, or Lido, provide a
liquid stake pool token in exchange for staking to their respective stake
pools (e.g. for every SOL staked to the Jito stake pool, delegators receive
jitoSOL). This makes staking positions of delegators liquid and allows them to
use it across Solana DeFi on protocols like Kamino, Marginfi, Meteora, and
more.  
  

![solana-stake-pools-jito-marinade-cogent-solblaze-lido-laine-sol-stake-pool-
manager-solana-multisig-
wallet](https://framerusercontent.com/images/9d4AbdLnYmUEFVJGdIUZpuufdU.png)

Like individual validators, stake pool managers also have authority keys to
control:

  * **Staker** : The Staker key has the authority to delegate or undelegate the stakes of the stake pool. In essence, the Staker is responsible for allocating the pool's resources to different validators. This is an operational role that needs to be active regularly.

  * **Manager** : The Manager key has the authority to modify the stake pool's parameters, such as the fee structure. This key is intended for administrative use, so it isn't frequently used. However, it is crucial for overall control and configuration of the stake pool.

Given that the Staker key is regularly used for routine operations and its
compromise doesn't immediately jeopardize the stake pool's health, it is often
managed with a simpler setup like a CLI wallet. On the other hand, the Manager
key, which has the authority to make significant changes to the stake pool's
parameters, demands more rigorous security measures - a multisig is more
appropriate to fulfill these security requirements.

With Squads, stake pool operators can spin up a multisig and delegate their
stake pool manager key to it via custom instructions. Similar to the withdraw
authority for individual validators, this setup provides all the benefits of
collective management and prevention against unauthorized actions or
compromised keys.

## Setup for Single Operators

Even if you are a single person managing a validator, you can enhance the
security of your withdraw authority key by creating a multisig setup involving
several wallets from different solutions. These could include both cold
wallets (like Ledger and OneKey) and hot wallets (such as Backpack and
Phantom). In an event where one wallet solution gets compromised, your
validator key would remain unaffected. This is due to:

  * The multisig holding the withdraw authority key;

  * The requirement of approvals from multiple keys to transfer the withdraw authority, change the commission, or withdraw rewards - a compromised private key cannot initiate these changes independently;

  * The ability to remove the compromised key with the other two hot/cold wallets and replace it with a new and fresh private key.  
  

![individual-validator-single-operator-hardware-wallet-multisig-setup-
withdraw-authority-key-validator-solana-
multisig](https://framerusercontent.com/images/eVY1kf6a17QoqP8QIpv6N7h2XsA.png)

This approach is certainly more complex, requiring the use of two keys every
time the withdraw authority is used or transferred. Nevertheless, it offers
the highest level of security for managing a validatorâs key.

## Secure Validator Management for a Robust Network

Just as secure program management is crucial for an antifragile Solana DeFi
ecosystem, secure validator management is essential for the Solana network. If
some validators were to have their keys compromised, impacting their
operations, it could shatter users' trust and discourage them from staking.
This scenario would be detrimental to both Solana and its validators.

With most validator teams and organizations operating remotely, it makes it
practically impossible to implement secure measures on their operations
without splitting the control of their valuable assets, such as the withdraw
authority key, among multiple stakeholders. Relying on one person/key leaves
room for many unknowns and facilitates malicious attacks. Opting for a
multisig solution like Squads is the best way to mitigate the risks associated
with traditional self-custody solutions like hardware wallets and move towards
a more decentralized approach.

If you're part of a team or an organization running a Solana validator and
seeking enhanced security measures for your operations, feel free to reach out
to us [here](https://t.me/SquadsProtocol_bot).  
  

_Acknowledgments: Thanks to Michael (_[_Laine_](https://laine.one/solana)
_/_[_Stakewiz.com_](https://stakewiz.com/) _) for feedback on earlier drafts
of this post._

  

### About Squads

Squads is a crypto company operations platform that simplifies management of
developer, creator, and treasury assets for teams building on Solana and SVM.
Open source, formally verified, immutable, Squads enables teams to secure
their on-chain assets in a multisig and jointly manage them.

**Learn more**

 _Squads:_[_https://squads.so/blog/what-is-
squads_](https://squads.so/blog/what-is-squads) _  
What are multisig wallets:_[_https://squads.so/blog/what-are-multisig-
wallets_](https://squads.so/blog/what-are-multisig-wallets) _  
Squads Protocol:_[_https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure_](https://squads.so/blog/solana-svm-smart-contract-wallet-
infrastructure) _  
Code:_[_https://github.com/Squads-Protocol/squads-
mpl_](https://github.com/Squads-Protocol/squads-mpl)

  

Continue reading

[![why-use-squads-why-multisig-solana-multisig-wallet-squads-leading-multi-
signature-solution-mpc-alternative-solana-secure-sol-for-company-squads-
protocol-
audited](https://framerusercontent.com/images/6S99P6ebVfLr6xzbo831NVDrCM.png)Why
Do Enterprises Use Squads For Their On-chain OperationsMarch 6, 2024](./why-
use-squads)[![how-to-create-mint-solana-spl-token-burn-mint-authority-solana-
multisig-squads-spl-token-
management](https://framerusercontent.com/images/YeQMBSozonTrL7s0M1gHdvMHtCw.png)Create
and Manage Solana (SPL) Tokens with SquadsDecember 13, 2023](./create-manage-
solana-spl-token)[![squads-solana-leading-multisig-spending-limits-treasury-
management-solana-multisig-wallet-squads-protocol-audited-formal-
verification](https://framerusercontent.com/images/2tyh01MPlECImwUoS4lpntdjCM.png)How
to Improve Treasury Operations with Spending LimitsNovember 29,
2023](./spending-limits)

[](../)

All rights reserved

Â© Squads Protocol 2024

Product

[Squads](../)

[Protocol](../protocol)

[Extension](../extension)

[Use Cases](../use-cases)

[Why Multisig](https://squads.so/blog/what-are-multisig-wallets)

Resources

[Github](https://github.com/Squads-Protocol)

[SDK](https://www.npmjs.com/package/@sqds/multisig)

[Documentation](https://docs.squads.so/main/basics/welcome-to-squads)

[Blog](../blog)

[Multisig vs MPC](https://squads.so/blog/mpc-wallets-risks-vs-multisig)

Company

[About](../about)

[Brand assets](../brand-assets)

[Twitter](https://twitter.com/squadsprotocol)

[Discord](https://discord.com/invite/YPXz64TrKs)

[Farcaster](https://warpcast.com/squads)

Legal

[Terms of Service](../legal/terms-of-service)

[Privacy Policy](../legal/privacy-policy)

[Contact us](https://discord.com/invite/YPXz64TrKs)

