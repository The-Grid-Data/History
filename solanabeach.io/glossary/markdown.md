Skip to mainIf you're seeing this message, that means **JavaScript has been
disabled on your browser** , please **enable JS** to make this app work.

[](/)

[](/)

Dashboard

Validators

Transactions

Blocks

Tokens

Supply

[Dashboard](/)

[Validators](/validators)

[Transactions](/transactions)

[Blocks](/blocks)

[Tokens](/tokens)

[Supply](/supply)

### Glossary

Search for slots, accounts, transactions, programs, tokens, and validators...

Technology

Slot Time

A slot refers to the period of time in which a slot leader produces ledger
entries. The minimum slot time is 400ms. We display the time it took the
current leader to ingest transactions and to produce a block.

Epoch

Epochs are the period of time for which a leader schedule is valid. Epochs are
made up of slots, hence, their duration varies between two to three days.

Weighted Skip Rate

Validators are assigned to leader slots during which they produce ledger
entries. The skip rate refers to the share of assigned leader slots that have
not been fulfilled by the respective validator. We calculate Skip Rate as
follows: (Number of skipped slots in current epoch / Number of scheduled
leader slots in the current epoch up to the current slot). The weighted skip
ratetakes the validators' stake into account and iscalculated as follows:
multiply each validators' skiprate with its' stake, sum up the results and
divide this value by the total active stake. For each validator we multiply
its skip rate by its stake, sum those results up, and then divided by the
total activated stake

Instructions

Instructions are the smallest unit of a program that clients can include in a
transaction. Instructions are passed to programs through the Solana runtime.
They are executed sequentially and atomically for each transaction.
Transactions can contain one or more instruction(s), should however one
instruction be invalid, the whole transaction fails. We decoded
someinstructions and labeled them e.g. 'transfer' for instructions that tell a
program to transfer a certain amount of SOL from one account to another.

Accounts inputs

Every public key constitutes an 'Account'. If the account only holds data, it
is referred to simply as an account. If it contains data that can be executed
upon, so code that can interpret instructions, it is referredto as a
'Program'. Hence, every 'Program' is an'Account', but not vice versa.

Staking APY

The Nominal Staking Annual Percentage Yield (APY) is what SOL token-holders
earn through staking their tokens. Since slot times vary and deviate from the
ideal length of 400 ms, the number of slots that will actually take place
within one year also varies. Staking rewards automatically compound with each
epoch. Therefore the APY is directly influenced by actual slot times. To best
reflect this, we take actual slot lengths (averaged for the past 24h) into
consideration when calculating the APY for SOL stakers. Please note that this
value does not take validator commission fees into account. We calculate the
Effective APY as:![Effective
APY](data:image/png;base64,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)

Copyright © 2024 - solanabeach.io[ __](https://twitter.com/solanabeach_io)

Contact Us[API](https://github.com/solana-
beach/api)[Imprint](/imprint)[Privacy](/privacy-policy)[Glossary](/glossary)

Cookies on the Beach

This website uses cookies to improve user experience. By using our website you
consent to all cookies in accordance with our Cookie Policy.  [ Read more
](/policy.html)

Performance

Targeting

Unclassified

Save & Close

Accept all

Decline all

Show details  Hide details

Cookie declaration

About cookies

Performance

Targeting

Unclassified

Performance cookies are used to see how visitors use the website, eg.
analytics cookies. Those cookies cannot be used to directly identify a certain
visitor.

Cookie report Name  |  Domain  |  Expiration  |  Description   
---|---|---|---  
_ga | .solanabeach.io |  2 years  |  This cookie name is associated with Google Universal Analytics - which is a significant update to Google's more commonly used analytics service. This cookie is used to distinguish unique users by assigning a randomly generated number as a client identifier. It is included in each page request in a site and used to calculate visitor, session and campaign data for the sites analytics reports.   
  
Targeting cookies are used to identify visitors between different websites,
eg. content partners, banner networks. Those cookies may be used by companies
to build a profile of visitor interests or show relevant ads on other
websites.

Cookie report Name  |  Domain  |  Expiration  |  Description   
---|---|---|---  
__cfduid | .solanabeach.io |  1 month  |  Cookie assoiated with sites using CloudFlare, used to speed up page load times. According to CloudFlare it is used to override any security restrictions based on the IP address the visitor is coming from. It does not contain any user identification information.   
  
Unclassified cookies are cookies that do not belong to any other category or
are in the process of categorization.

Cookie report Name  |  Domain  |  Expiration  |  Description   
---|---|---|---  
_ga_DDV5S1ZHNC | .solanabeach.io |  2 years  |   
  
Cookies are small text files that are placed on your computer by websites that
you visit. Websites use cookies to help users navigate efficiently and perform
certain functions. Cookies that are required for the website to operate
properly are allowed to be set without your permission. All other cookies need
to be approved before they can be set in the browser. You can change your
consent to cookie usage at any time on our Privacy Policy page.

Cookies consent ID:

Cookie [report](https://cookie-script.com/cookie-
report?identifier=04b70854c5afd3c8a61f14ae37a83348) created by [Cookie-
Script](https://cookie-script.com)

×

