Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

  1. [Home](/en/)/
  2. [Bug bounty](/en/bug-bounty/)

Open for submissions

# Bug Bounty Program

Earn up to 250,000 USD and a place on the leaderboard by finding protocol,
client and Solidity bugs affecting the Ethereum network.

[Submit a bug(opens in a new tab)](https://forms.gle/Gnh4gzGh66Yc3V7G8)Read
rules

  * 1

ga

[In place number 1 with 46100 pointsGuido Vranken (See Github Profile)(opens
in a new tab)](https://github.com/guidovranken)

46100 points

  * 2

pa

[In place number 2 with 42400 pointsprotolambda (See Github Profile)(opens in
a new tab)](https://github.com/protolambda)

42400 points

  * 3

ha

[In place number 3 with 40000 pointsMartin Holst Swende (See Github
Profile)(opens in a new tab)](https://github.com/holiman)

40000 points

  * 4

sa

[In place number 4 with 35000 pointsSam Sun (See Github Profile)(opens in a
new tab)](https://github.com/samczsun)

35000 points

  * 5

In place number 5 with 31000 pointsnrv (@nervoir)

31000 points

See full leaderboards

Clients featured in the bounties

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fbesu.cd867de4.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Ferigon.14d44b2d.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fgeth.3aab6f0d.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fnethermind.faad9340.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Flighthouse-
light.a4c06b89.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Flodestar.07807ed0.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fnimbus-
cloud.5e4c680a.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fprysm.75acb4e1.png&w=128&q=75)

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fteku-
dark.17d2ef40.png&w=128&q=75)

## In Scope

Our bug bounty program spans end-to-end: from soundness of protocols (such as
the blockchain consensus model, the wire and p2p protocols, proof of stake,
etc.) and protocol/implementation compliance to network security and consensus
integrity. Classical client security as well as security of cryptographic
primitives are also part of the program. When in doubt, send an email to
bounty@ethereum.org and ask us. You may also submit a disclosure/vulnerability
directly to [bounty@ethereum.org(opens in a new
tab)](mailto:bounty@ethereum.org), in which case we ask that you encrypt the
message using our [PGP Key(opens in a new
tab)](https://ethereum.org/security_at_ethereum.org.asc)

### Specification bugs

The Ethereum Specifications detail the design rationale for the Execution
Layer and Consensus Layer.

[Consensus Layer Specifications(opens in a new
tab)](https://github.com/ethereum/consensus-specs)  
[Execution Layer Specifications(opens in a new
tab)](https://github.com/ethereum/execution-specs)  

It might be helpful to check out the following annotations:

  * [Ben Edgington's annotated spec(opens in a new tab)](https://benjaminion.xyz/eth2-annotated-spec/)
  * [Vitalik Buterin's annotated spec(opens in a new tab)](https://github.com/ethereum/annotated-spec)

#### Types of bugs

  * Safety/finality-breaking bugs
  * Denial of service (DOS) vectors
  * Inconsistencies in assumptions, like situations where honest validators can be slashed
  * Calculation or parameter inconsistencies

#### Specification documents

[Beacon Chain(opens in a new tab)](https://github.com/ethereum/consensus-
specs/blob/dev/specs/phase0/beacon-chain.md)

↗

[Fork choice(opens in a new tab)](https://github.com/ethereum/consensus-
specs/blob/dev/specs/phase0/fork-choice.md)

↗

[Solidity deposit contract(opens in a new
tab)](https://github.com/ethereum/consensus-
specs/blob/dev/specs/phase0/deposit-contract.md)

↗

[Peer-to-peer networking(opens in a new
tab)](https://github.com/ethereum/consensus-
specs/blob/dev/specs/phase0/p2p-interface.md)

↗

### Client bugs

Clients run the Ethereum Network, and they need to follow the logic set out in
the specification and be secure against potential attacks. The bugs we want to
find are related to the implementation of the protocol.

Currently execution layer clients (Besu, Erigon, Geth and Nethermind) and
consensus layer clients (Lighthouse, Lodestar, Nimbus, Teku and Prysm) are
included in the Bug Bounty Program. More clients may be added as they complete
audits and become production ready. Currently, [c-kzg-4844(opens in a new
tab)](https://github.com/ethereum/c-kzg-4844) and [go-kzg-4844(opens in a new
tab)](https://github.com/crate-crypto/go-kzg-4844) are also included in the
bug bounty program.

#### Types of bugs

  * Spec non-compliance issues
  * Unexpected crashes, RCE or denial of service (DOS) vulnerabilities
  * Any issues causing irreparable consensus splits from the rest of the network

#### Helpful links

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fbesu.cd867de4.png&w=48&q=75)

[Besu(opens in a new tab)](https://besu.hyperledger.org/en/stable/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Ferigon.14d44b2d.png&w=48&q=75)

[Erigon(opens in a new tab)](https://github.com/ledgerwatch/erigon)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fgeth.3aab6f0d.png&w=48&q=75)

[Geth(opens in a new tab)](https://geth.ethereum.org/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Flighthouse-
light.a4c06b89.png&w=48&q=75)

[Lighthouse(opens in a new tab)](https://lighthouse-book.sigmaprime.io/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Flodestar.07807ed0.png&w=48&q=75)

[Lodestar(opens in a new tab)](https://chainsafe.github.io/lodestar/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fnimbus-
cloud.5e4c680a.png&w=48&q=75)

[Nimbus(opens in a new tab)](https://our.status.im/tag/nimbus/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fnethermind.faad9340.png&w=48&q=75)

[Nethermind(opens in a new tab)](https://docs.nethermind.io/nethermind/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fprysm.75acb4e1.png&w=48&q=75)

[Prysm(opens in a new tab)](https://prylabs.net/)

↗

![](/_next/image/?url=%2F_next%2Fstatic%2Fmedia%2Fteku-
dark.17d2ef40.png&w=48&q=75)

[Teku(opens in a new tab)](https://pegasys.tech/teku)

↗

### Solidity bugs

See the Solidity SECURITY.MD for more details about what is included in this
scope.

Solidity does not hold security guarantees regarding compilation of untrusted
input – and we do not issue rewards for crashes of the solc compiler on
maliciously generated data.

#### Helpful links

[SECURITY.md(opens in a new
tab)](https://github.com/ethereum/solidity/blob/develop/SECURITY.md)

### Deposit Contract bugs

The specifications and source code of the Beacon Chain Deposit Contract is
part of the bug bounty program.

#### Helpful links

[Deposit Contract Specifications(opens in a new
tab)](https://github.com/ethereum/consensus-
specs/blob/dev/specs/phase0/deposit-contract.md)  
[Deposit Contract Source Code(opens in a new
tab)](https://github.com/ethereum/consensus-
specs/blob/dev/solidity_deposit_contract/deposit_contract.sol)

## Out of scope

Only the targets listed under in-scope are part of the Bug Bounty Program.
This means that for example our infrastructure; such as webpages, dns, email
etc, are not part of the bounty-scope. ERC20 contract bugs are typically not
included in the bounty scope. However, we can help reach out to affected
parties, such as authors or exchanges in such cases. ENS is maintained by the
ENS foundation, and is not part of the bounty scope. Vulnerabilities requiring
the user to have publicly exposed an API, such as JSON-RPC or the Beacon API,
is out of scope of the bug bounty program.

## Submit a bug

For each valid bug you find you’ll earn rewards. The quantity of rewards
awarded will vary depending on Severity. The severity is calculated according
to the OWASP risk rating model based on Impact on the Ethereum Network and
Likelihood. [View OWASP method(opens in a new
tab)](https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology)

The EF will also provide rewards based on:

**Quality of description** : Higher rewards are paid for clear, well-written
submissions.

**Quality of reproducibility** : A Proof of Concept (POC) must be included to
be eligible for rewards. Please include test code, scripts and detailed
instructions. The easier it is for us to reproduce and verify the
vulnerability, the higher the reward.

**Quality of fix** , if included: Higher rewards are paid for submissions with
clear description of how to fix the issue.

Up to 2,000 USD

## Low

Up to 2,000 USD

Up to 1,000 points

* * *

Severity

  * Low impact, medium likelihood
  * Medium impact, low likelihood

* * *

Example

Attacker can sometimes put a node in a state that causes it to drop one out of
every one hundred attestations made by a validator

[Submit low risk bug(opens in a new tab)](https://forms.gle/Gnh4gzGh66Yc3V7G8)

Up to 10,000 USD

## Medium

Up to 10,000 USD

Up to 5,000 points

* * *

Severity

  * High impact, low likelihood
  * Medium impact, medium likelihood
  * Low impact, high likelihood

* * *

Example

Attacker can successfully conduct eclipse attacks on nodes with peer-ids with
4 leading zero bytes

[Submit medium risk bug(opens in a new
tab)](https://forms.gle/Gnh4gzGh66Yc3V7G8)

Up to 50,000 USD

## High

Up to 50,000 USD

Up to 10,000 points

* * *

Severity

  * High impact, medium likelihood
  * Medium impact, high likelihood

* * *

Example

Attacker can successfully partition large parts of the network, and it is
trivial for an attacker to trigger the vulnerability

[Submit high risk bug(opens in a new
tab)](https://forms.gle/Gnh4gzGh66Yc3V7G8)

Up to 250,000 USD

## Critical

Up to 250,000 USD

Up to 25,000 points

* * *

Severity

  * High impact, high likelihood

* * *

Example

Attacker can successfully conduct remote code execution in a majority client,
and it is trivial for an attacker to trigger the vulnerability

[Submit critical risk bug(opens in a new
tab)](https://forms.gle/Gnh4gzGh66Yc3V7G8)

## Bug hunting rules

 _The bug bounty program is an experimental and discretionary rewards program
for our active Ethereum community to encourage and reward those who are
helping to improve the platform. It is not a competition. You should know that
we can cancel the program at any time, and awards are at the sole discretion
of Ethereum Foundation bug bounty panel. In addition, we are not able to issue
awards to individuals who are on sanctions lists or who are in countries on
sanctions lists (e.g. North Korea, Iran, etc). Local laws require us to ask
for proof of your identity. You are responsible for all taxes. All awards are
subject to applicable law. Finally, your testing must not violate any law or
compromise any data that is not yours and must take place on local running
testnets._

  * Issues without a POC or that have already been submitted by another user or are already known to spec and client maintainers are not eligible for bounty rewards.
  * Public disclosure of a vulnerability or reporting it to other parties without prior agreement makes it ineligible for a bounty.
  * Employees and contractors of the Ethereum Foundation or client teams in scope of the bounty program may participate in the program only in the accrual of points and will not receive monetary rewards.
  * Ethereum bounty program considers a number of variables in determining rewards. Determinations of eligibility, score and all terms related to an award are at the sole and final discretion of the Ethereum Foundation bug bounty panel.

## Execution Layer Bug Bounty leaderboard

Find execution layer bugs to get added to this leaderboard

  * 1

ha

[In place number 1 with 37500 pointsMartin Holst Swende (See Github
Profile)(opens in a new tab)](https://github.com/holiman)

37500 points

  * 2

sa

[In place number 2 with 35000 pointsSam Sun (See Github Profile)(opens in a
new tab)](https://github.com/samczsun)

35000 points

  * 3

In place number 3 with 31000 pointsnrv (@nervoir)

31000 points

  * 4

ga

[In place number 4 with 28250 pointsGuido Vranken (See Github Profile)(opens
in a new tab)](https://github.com/guidovranken)

28250 points

  * 5

ca

[In place number 5 with 23500 pointsChainSecurity (See Github Profile)(opens
in a new tab)](https://github.com/chainsecurity)

23500 points

  * 6

ja

[In place number 6 with 20500 pointsJuno Im (See Github Profile)(opens in a
new tab)](https://github.com/junorouse)

20500 points

  * 7

ua

[In place number 7 with 20000 pointsYoonho Kim (team Hithereum) (See Github
Profile)(opens in a new tab)](https://github.com/uknowy)

20000 points

  * 8

ja

[In place number 8 with 20000 pointsJohn Youngseok Yang (Software Platform
Lab) (See Github Profile)(opens in a new tab)](https://github.com/johnyangk)

20000 points

  * 9

pa

[In place number 9 with 17000 pointsPeckShield (See Github Profile)(opens in a
new tab)](https://github.com/peckshield)

17000 points

  * 10

ia

[In place number 10 with 15000 pointsItsUnixIKnowThis (See Github
Profile)(opens in a new tab)](https://github.com/itsunixiknowthis)

15000 points

  * 11

ca

[In place number 11 with 15000 pointsBertrand Masius (See Github
Profile)(opens in a new tab)](https://github.com/catageek)

15000 points

  * 12

In place number 12 with 13000 pointsBob Conan

13000 points

  * 13

ta

[In place number 13 with 12500 pointsTin (See Github Profile)(opens in a new
tab)](https://github.com/tintinweb)

12500 points

  * 14

In place number 14 with 12500 pointsRalph Pichler

12500 points

  * 15

la

[In place number 15 with 11000 pointsŁukasz Matczak (See Github Profile)(opens
in a new tab)](https://github.com/lukaszmatczak)

11000 points

  * 16

In place number 16 with 10000 pointsHeilman/Marcus/Goldberg

10000 points

  * 17

ja

[In place number 17 with 10000 pointsJonas Nick (See Github Profile)(opens in
a new tab)](https://github.com/jonasnick)

10000 points

  * 18

ja

[In place number 18 with 10000 pointsJohn Toman (See Github Profile)(opens in
a new tab)](https://github.com/jtoman)

10000 points

  * 19

In place number 19 with 8000 pointsSebastian Henningsen

8000 points

  * 20

In place number 20 with 7500 pointsDominic Brütsch

7500 points

  * 21

Ha

[In place number 21 with 5000 pointsHarry Roberts (See Github Profile)(opens
in a new tab)](https://github.com/HarryR)

5000 points

  * 22

pa

[In place number 22 with 5000 pointsPeter Stöckli (See Github Profile)(opens
in a new tab)](https://github.com/p-)

5000 points

  * 23

Da

[In place number 23 with 5000 pointsNeville Grech (See Github Profile)(opens
in a new tab)](https://github.com/Dedaub)

5000 points

  * 24

Ea

[In place number 24 with 5000 pointsEthHead (See Github Profile)(opens in a
new tab)](https://github.com/EthHead)

5000 points

  * 25

ia

[In place number 25 with 5000 pointsiosiro (See Github Profile)(opens in a new
tab)](https://github.com/iosiro)

5000 points

  * 26

aa

[In place number 26 with 3500 pointsAlex Beregszaszi (See Github
Profile)(opens in a new tab)](https://github.com/axic)

3500 points

  * 27

Sa

[In place number 27 with 2500 pointsSergio Demian Lerner (See Github
Profile)(opens in a new tab)](https://github.com/SergioDemianLerner)

2500 points

  * 28

da

[In place number 28 with 2500 pointsDaniel Perez (See Github Profile)(opens in
a new tab)](https://github.com/danhper)

2500 points

  * 29

ea

[In place number 29 with 2500 pointsOP Labs (See Github Profile)(opens in a
new tab)](https://github.com/ethereum-optimism)

2500 points

  * 30

ya

[In place number 30 with 2000 pointsYaron Velner (See Github Profile)(opens in
a new tab)](https://github.com/yaronvel)

2000 points

  * 31

wa

[In place number 31 with 2000 pointsWhit Jackson (See Github Profile)(opens in
a new tab)](https://github.com/whitj00)

2000 points

  * 32

In place number 32 with 2000 pointsMing Chuan Lin

2000 points

  * 33

ma

[In place number 33 with 2000 pointsMelonport team (See Github Profile)(opens
in a new tab)](https://github.com/melonport)

2000 points

  * 34

ma

[In place number 34 with 2000 pointsMaurelian (See Github Profile)(opens in a
new tab)](https://github.com/maurelian)

2000 points

  * 35

Ca

[In place number 35 with 2000 pointsChristoph Jentzsch (See Github
Profile)(opens in a new tab)](https://github.com/Cjentzsch)

2000 points

  * 36

ha

[In place number 36 with 1500 pointsHwanjo Heo (See Github Profile)(opens in a
new tab)](https://github.com/hwanjo)

1500 points

  * 37

Ba

[In place number 37 with 1500 pointsBlockTrident (See Github Profile)(opens in
a new tab)](https://github.com/BlockTrident)

1500 points

  * 38

Da

[In place number 38 with 1200 pointsDVP (dvpnet.io) (See Github Profile)(opens
in a new tab)](https://github.com/DVPNET)

1200 points

  * 39

In place number 39 with 1000 pointsVasily Vasiliev

1000 points

  * 40

ta

[In place number 40 with 1000 pointstalko (See Github Profile)(opens in a new
tab)](https://github.com/talko)

1000 points

  * 41

sa

[In place number 41 with 1000 pointsSteve Waldman (See Github Profile)(opens
in a new tab)](https://github.com/swaldman)

1000 points

  * 42

pa

[In place number 42 with 1000 pointsPanu Kekäläinen (See Github Profile)(opens
in a new tab)](https://github.com/ptk)

1000 points

  * 43

ma

[In place number 43 with 1000 pointsJosselin Feist (See Github Profile)(opens
in a new tab)](https://github.com/montyly)

1000 points

  * 44

ha

[In place number 44 with 1000 pointsHenrit (See Github Profile)(opens in a new
tab)](https://github.com/henrit)

1000 points

  * 45

Ba

[In place number 45 with 1000 pointsMarc Bartlett (See Github Profile)(opens
in a new tab)](https://github.com/BlameByte)

1000 points

  * 46

In place number 46 with 1000 pointsBarry Whitehat

1000 points

  * 47

ba

[In place number 47 with 1000 pointsLucas Ryan (See Github Profile)(opens in a
new tab)](https://github.com/badmofo)

1000 points

  * 48

aa

[In place number 48 with 1000 pointsAlex Groce (See Github Profile)(opens in a
new tab)](https://github.com/agroce)

1000 points

  * 49

na

[In place number 49 with 750 pointsDaniel Briskin (See Github Profile)(opens
in a new tab)](https://github.com/n0thingness)

750 points

  * 50

da

[In place number 50 with 750 pointsDaenam Kim (See Github Profile)(opens in a
new tab)](https://github.com/daenamkim)

750 points

  * 51

In place number 51 with 500 pointsMyeongjae Lee

500 points

  * 52

In place number 52 with 500 pointsMarcin Noga (Cisco/Talos Security)

500 points

  * 53

In place number 53 with 500 pointsjazzybedi

500 points

  * 54

fa

[In place number 54 with 500 pointsFeeker - 360 ESG Codesafe Team (See Github
Profile)(opens in a new tab)](https://github.com/feeker)

500 points

  * 55

ea

[In place number 55 with 500 pointsJonathan Brown (See Github Profile)(opens
in a new tab)](https://github.com/ethernomad)

500 points

  * 56

da

[In place number 56 with 500 pointsDavid Murdoch (See Github Profile)(opens in
a new tab)](https://github.com/davidmurdoch)

500 points

  * 57

wa

[In place number 57 with 500 pointsAlexander Wade (See Github Profile)(opens
in a new tab)](https://github.com/wadeAlexC)

500 points

  * 58

ga

[In place number 58 with 200 pointsLuis Schliesske (See Github Profile)(opens
in a new tab)](https://github.com/gitpusha)

200 points

## Consensus Layer Bug Bounty leaderboard

Find consensus layer bugs to get added to this leaderboard

  * 1

pa

[In place number 1 with 42400 pointsprotolambda (See Github Profile)(opens in
a new tab)](https://github.com/protolambda)

42400 points

  * 2

ca

[In place number 2 with 19650 pointsQuan Thoi Minh Nguyen (See Github
Profile)(opens in a new tab)](https://github.com/cryptosubtlety)

19650 points

  * 3

ja

[In place number 3 with 18700 pointsJonny Rhea (See Github Profile)(opens in a
new tab)](https://github.com/jrhea)

18700 points

  * 4

ga

[In place number 4 with 17850 pointsGuido Vranken (See Github Profile)(opens
in a new tab)](https://github.com/guidovranken)

17850 points

  * 5

In place number 5 with 10000 pointsscio

10000 points

  * 6

sa

[In place number 6 with 9000 pointsGrandine team (See Github Profile)(opens in
a new tab)](https://github.com/sifraitech)

9000 points

  * 7

ka

[In place number 7 with 6000 pointsOnur Kılıç (See Github Profile)(opens in a
new tab)](https://github.com/kilic)

6000 points

  * 8

aa

[In place number 8 with 5000 pointsAntoine Toulme (See Github Profile)(opens
in a new tab)](https://github.com/atoulme)

5000 points

  * 9

Va

[In place number 9 with 5000 pointsVulnerabilityX (See Github Profile)(opens
in a new tab)](https://github.com/Vulnerability-X)

5000 points

  * 10

aa

[In place number 10 with 4000 pointsAntonio Sanso (See Github Profile)(opens
in a new tab)](https://github.com/asanso)

4000 points

  * 11

ia

[In place number 11 with 2850 pointsItsUnixIKnowThis (See Github
Profile)(opens in a new tab)](https://github.com/itsunixiknowthis)

2850 points

  * 12

Aa

[In place number 12 with 2500 pointsAlexander Sadovskyi (See Github
Profile)(opens in a new tab)](https://github.com/AlexSSD7)

2500 points

  * 13

ta

[In place number 13 with 2500 pointstintin (See Github Profile)(opens in a new
tab)](https://github.com/tintinweb)

2500 points

  * 14

ha

[In place number 14 with 2500 pointsMartin Holst Swende (See Github
Profile)(opens in a new tab)](https://github.com/holiman)

2500 points

  * 15

In place number 15 with 1750 pointsAkincibor

1750 points

  * 16

ma

[In place number 16 with 200 pointsJim McDonald (See Github Profile)(opens in
a new tab)](https://github.com/mcdee)

200 points

## Frequently asked questions

###

What should a good vulnerability submission look like?

See a real example of a quality vulnerability submission.

More

**Description:** Remote Denial-of-service using non-validated blocks

**Attack scenario:** An attacker can send blocks that may require a high
amount of computation (the maximum gasLimit) but has no proof-of-work. If the
attacker sends blocks continuously, the attacker may force the victim node to
100% CPU utilization.

**Impact:** An attacker can abuse CPU utilization on remote nodes, possibly
causing full DoS.

**Components:** Go client version v0.6.8

**Reproduction:** Send a block to a Go node that contains many txs but no
valid PoW.

**Details:** Blocks are validated in the method `Process(Block, dontReact)`.
This method performs expensive CPU-intensive tasks, such as executing
transactions (`sm.ApplyDiff`) and afterward it verifies the proof-of-work
(`sm.ValidateBlock()`). This allows an attacker to send blocks that may
require a high amount of computation (the maximum `gasLimit`) but has no
proof-of-work. If the attacker sends blocks continuously, the attacker may
force the victim node to 100% CPU utilization.

**Fix:** Invert the order of the checks.

###

Is the bug bounty program is time limited?

No.

More

No end date is currently set. See [the Ethereum Foundation blog(opens in a new
tab)](https://blog.ethereum.org/) for the latest news.

###

How are bounties paid out?

Rewards are paid out in ETH or DAI.

More

Rewards are paid out in ETH or DAI after the submission has been validated,
usually a few days later. Local laws require us to ask for **proof of your
identity**. In addition, we will need your ETH address.

###

Can I donate my reward to charity?

Yes!

More

We can donate your reward to an established charitable organization of your
choice.

###

I reported an issue / vulnerability but have not received a response!

Please allow a few days for someone to respond to your submission.

More

We aim to respond to submissions as fast as possible. Feel free to email us at
[bounty@ethereum.org(opens in a new tab)](mailto:bounty@ethereum.org) if you
have not received a response within a day or two.

###

I want to be anonymous / I do not want my name on the leader board.

You can do this, but it might make you ineligble for rewards.

More

Submitting anonymously or with a pseudonym is OK, but will make you ineligible
for ETH/DAI rewards. To be eligible for ETH/DAI rewards, we require your real
name and a proof of your identity. Donating your bounty to a charity doesn’t
require your identity.

Please let us know if you do not want your name/nick displayed on the leader
board.

###

What are the points in the leaderboard?

Every found vulnerability / issue is assigned a score

More

Every found vulnerability / issue is assigned a score. Bounty hunters are
ranked on our leaderboard by total points.

###

Do you have a PGP key?

Yes. Expand for details.

More

Please use `AE96 ED96 9E47 9B00 84F3 E17F E88D 3334 FA5F 6A0A`

[PGP Key(opens in a new
tab)](https://ethereum.org/security_at_ethereum.org.asc)

## Questions?

Email us: [bounty@ethereum.org(opens in a new
tab)](mailto:bounty@ethereum.org)

### Was this page helpful?

YesNo

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

