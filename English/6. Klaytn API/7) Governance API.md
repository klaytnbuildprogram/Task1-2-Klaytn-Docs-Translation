# Governance API

For the governance of the network, Klaytn provides the following APIs under governance namespace.

In Klaytn, there are three different governance modes.

none: All nodes participating in the network have the right to change the configuration.

single: Only one designated node has the right to change the configuration.

ballot: All nodes which have voting power can vote for a change. When more than half of total voting power gathered, the vote passes.

## governance_vote
The vote method submits a new vote. If the node has the right to vote based on governance mode, the vote can be placed. If not, an error message will be returned and the vote will be ignored.

Parameters

Key : Name of the configuration setting to be changed. Key has the form of domain.field

Value : Various types of value for each key. 

Key

Description

"governance.governancemode"

STRING. One of the three governance modes. "none", "single", "ballot"

"governance.governingnode"

ADDRESS. Designated governing node's address. It only works if the governance mode is "single" e.g.,"0xe733cb4d279da696f30d470f8c04decb54fcb0d2"

"governance.unitprice"

NUMBER. Price of unit gas. e.g., 25000000000

"governance.addvalidator"

ADDRESS. Address of a new validator candidate. e.g., 0xe733cb4d279da696f30d470f8c04decb54fcb0d2

"governance.removevalidator"

ADDRESS. Address of a current validator which need to be removed. e.g., 0xe733cb4d279da696f30d470f8c04decb54fcb0d2

"istanbul.epoch"

NUMBER. A period in which votes are gathered in blocks. When an epoch end, all votes which haven't been passed will be cleared. e.g., 86400

"istanbul.committeesize"

NUMBER. The number of validators in a committee.(sub in chain configuration) e.g., 7

"reward.mintingamount"

STRING. Amount of Peb minted when a block is generated. Double quotation marks are needed for a value. e.g., "9600000000000000000"

"reward.ratio"

STRING. Distribution rate for a CN/PoC/KIR separated by "/". The sum of all values has to be 100. e.g., "34/54/12" meaning CN 34%, PoC 54%, KiR 12%

"reward.useginicoeff"

BOOL. Use the Gini coefficient or not. true, false

"reward.deferredtxfee"

BOOL. The way of giving transaction fee to a proposer. If true, it means the tx fee will be summed up with block reward and distributed to the proposer, KIR and PoC. If not, all tx fee will be given to the proposer. true, false

"reward.minimumstake"

STRING. Amount of Klay required to be a CN (Consensus Node). Double quotation marks are needed for a value. e.g., "5000000"

Return Value

Type

Description

String

Result of vote submission

Example

> governance.vote ("governance.governancemode", "ballot")
"Your vote was successfully placed."
​
> governance.vote ("governance.governingnode", "0x12345678990123456789901234567899012345678990")
"Your vote was successfully placed."
​
> governance.vote("istanbul.epoch", 604800)
"Your vote was successfully placed."
​
> governance.vote("governance.unitprice", 25000000000)
"Your vote was successfully placed."
​
> governance.vote("istanbul.committeesize", 7)
"Your vote was successfully placed."
​
> governance.vote("reward.mintingamount", "9600000000000000000")
"Your vote was successfully placed."
​
> governance.vote("reward.ratio", "40/30/30")
"Your vote was successfully placed."
​
> governance.vote("reward.useginicoeff", false)
"Your vote was successfully placed."
​
// If wrong data are given
> governance.vote("reward.ratio", 100)
"Your vote couldn't be placed. Please check your vote's key and value"
​
> governance.vote("governance.governingnode", 1234)
"Your vote couldn't be placed. Please check your vote's key and value"
​
// when `governancemode` is "single" and the node is not `governingnode`
> governance.vote("governance.governancemode", "ballot")
"You don't have the right to vote"
## governance_showTally
The showTally property provides the current tally of governance votes. It shows the aggregated approval rate in percentage. When it goes over 50%, the vote passes.

Parameters

None

Return Value

Type

Description

Tally

Each vote's value and approval rate in percentage

Example

> governance.showTally
[{
    ApprovalPercentage: 36.2,
    Key: "unitprice",
    Value: 25000000000
}, {
    ApprovalPercentage: 72.5,
    Key: "mintingamount",
    Value: "9600000000000000000"
}]
## governance_totalVotingPower
The totalVotingPower property provides the sum of all voting power that CNs have. Each CN has 1.0 ~ 2.0 voting power. In "none", "single" governance mode, totalVotingPower don't provide any information.

Parameters

None

Return Value

Type

Description

Float

Total Voting Power or error message

Example

// In "ballot" governance mode
> governance.totalVotingPower
32.452
​
// In "none", "single" governance mode
> governance.totalVotingPower
"In current governance mode, voting power is not available"
## governance_myVotingPower
The myVotingPower property provides the voting power of the node. The voting power can be 1.0 ~ 2.0. In "none", "single" governance mode, totalVotingPower don't provide any information.

Parameters

None

Return Value

Type

Description

Float

Node's Voting Power or error message

Example

// In "ballot" governance mode
> governance.myVotingPower
1.323
​
// In "none", "single" governance mode
> governance.myVotingPower
"In current governance mode, voting power is not available"
## governance_myVotes
The myVotes property provides my vote information in the epoch. Each vote is stored in a block when the user's node generates a new block. After current epoch ends, this information is cleared.

Parameters

None

Return Value

Type

Description

Vote List

Node's Voting status in the epoch
- BlockNum: The block number that this vote is stored
- Casted: If this vote is stored in a block or not
- Key/Value: The content of the vote

Example

> governance.vote("governance.governancemode", "ballot")
"Your vote was successfully placed."
​
> governance.myVotes
[{
    BlockNum: 403,
    Casted: true,
    Key: "governance.governancemode",
    Value: "ballot"
}]
## governance_chainConfig
The chainConfig property provides current chain configuration information.

Parameters

None

Return Value

Type

Description

JSON

Current chain configuration

Example

> governance.chainConfig
{
  chainId: 1001,
  deriveShaImpl: 2,
  governance: {
    governanceMode: "ballot",
    governingNode: "0xe733cb4d279da696f30d470f8c04decb54fcb0d2",
    reward: {
      deferredTxFee: true,
      minimumStake: 5000000,
      mintingAmount: 9600000000000000000,
      proposerUpdateInterval: 3600,
      ratio: "34/54/12",
      stakingUpdateInterval: 20,
      useGiniCoeff: false
    }
  },
  istanbul: {
    epoch: 20,
    policy: 2,
    sub: 1
  },
  unitPrice: 25000000000
}
## governance_nodeAddress
The nodeAddress property provides the address of the node that a user is using. It is derived from the nodekey and used to sign consensus messages. And the value of "governingnode" has to be one of validator's node address.

Parameters

None

Return Value

Type

Description

ADDRESS

20 BYTE address of a node

Example

> governance.nodeAddress
"0xe733cb4d279da696f30d470f8c04decb54fcb0d2"
## governance_itemsAt
The itemsAt returns governance items at specific block. It is the result of previous voting of the block and used as configuration for chain at the given block number.

Parameters

Type

Description

QUANTITY | TAG

Integer of a block number, or the string "earliest", "latest" or "pending", as in the default block parameter.

Return Value

Type

Description

JSON

governance items

Example

> governance.itemsAt(89)
{
 governance.governancemode: "single",
 governance.governingnode: "0x7bf29f69b3a120dae17bca6cf344cf23f2daf208",
 governance.unitprice: 25000000000,
 istanbul.committeesize: 13,
 istanbul.epoch: 30,
 istanbul.policy: 2,
 reward.deferredtxfee: true,
 reward.minimumstake: "5000000",
 reward.mintingamount: "9600000000000000000",
 reward.proposerupdateinterval: 30,
 reward.ratio: "34/54/12",
 reward.stakingupdateinterval: 60,
 reward.useginicoeff: true
}