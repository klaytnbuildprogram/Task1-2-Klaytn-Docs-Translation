# Klaytn Gas Table

## Gas and Unit Price Overview
Every action that changes the state of the blockchain requires gas. When a node processes user's transaction such as sending KLAY, using ERC-20 tokens, or executing a contract, the user has to pay for the computation and storage usage. The amount of payment is decided by the amount of Gas required.

Gas is a measuring unit representing how much calculation is needed to process the user's transaction.

As the transaction fee is paid in KLAY, the total amount of KLAY to be paid by a user is calculated as below,

transaction fee = the amount of gas * unit price (KLAY)
where the unit price is the price for a single gas. The unit price (also called gas price) is set in the system by the governance.

In Ethereum, users set the gas price for each transaction, and miners choose which transactions to be included in their block to maximize their reward. It is something like bidding for limited resources. This approach has been working because it is market-based. However, the transaction cost fluctuates and often becomes too high to guarantee the execution.

To solve the problem, Klaytn is using a fixed unit price (25 ston) and the price can be adjusted by the governance council. This policy ensures that every transaction will be handled equally and be guaranteed to be executed. Therefore, users do not need to struggle to determine the right unit price.

## Klaytn's Gas table
Basically, Klaytn is keeping compatibility with Ethereum. So Klaytn's gas table is pretty similar with that of Ethereum. But because of the existence of unique features of Klaytn, there are several new constants for those features.

### Common Fee
Item

Gas

Description

G_zero

0

Nothing paid for operations of the set Wzero

G_base

2

Amount of gas to pay for operations of the set Wbase

G_verylow

3

Amount of gas to pay for operations of the set Wverylow

G_low

5

Amount of gas to pay for operations of the set Wlow

G_mid

8

Amount of gas to pay for operations of the set Wmid

G_high

10

Amount of gas to pay for operations of the set Whigh

G_blockhash

20

Payment for BLOCKHASH operation

G_extcode

700

Amount of gas to pay for operations of the set Wextcode

G_balance

400

Amount of gas to pay for a BALANCE operation

G_sload

200

Paid for a SLOAD operation

G_jumpdest

1

Paid for a JUMPDEST operation

G_sset

20000

Paid for an SSTORE operation when the storage value is set to non-zero from zero

G_sreset

5000

Paid for an SSTORE operation when the storage value’s zeroness remains unchanged or is set to zero

G_sclear

15000

Refund given (added into refund counter) when the storage value is set to zero from non-zero

R_selfdestruct

24000

Refund given (added into refund counter) for self-destructing an account

G_selfdestruct

5000

Amount of gas to pay for a SELFDESTRUCT operation

G_create

32000

Paid for a CREATE operation

G_codedeposit

200

Paid per byte for a CREATE operation to succeed in placing code into state

G_call

700

Paid for a CALL operation

G_callvalue

9000

Paid for a non-zero value transfer as part of the CALL operation

G_callstipend

2300

A stipend for the called contract subtracted from Gcallvalue for a non-zero value transfer

G_newaccount

25000

Paid for a CALL or SELFDESTRUCT operation which creates an account

G_exp

10

Partial payment for an EXP operation

G_expbyte

50

Partial payment when multiplied by dlog256(exponent)e for the EXP operation

G_memory

3

Paid for every additional word when expanding memory

G_txcreate

32000

Paid by all contract-creating transactions

G_transaction

21000

Paid for every transaction

G_log

375

Partial payment for a LOG operation

G_logdata

8

Paid for each byte in a LOG operation’s data

G_logtopic

375

Paid for each topic of a LOG operation

G_sha3

30

Paid for each SHA3 operation

G_sha3word

6

Paid for each word (rounded up) for input data to a SHA3 operation

G_copy

3

Partial payment for *COPY operations, multiplied by words copied, rounded up

G_blockhash

20

Payment for BLOCKHASH operation

G_extcodehash

400

Paid for getting keccak256 hash of a contract's code

G_create2

32000

Paid for opcode CREATE2 which bahaves identically with CREATE but use different arguemnts

### Precompiled Contracts
Precompiled contracts are special kind of contracts which usually perform complex cryptographic computations and are initiated by other contracts.

Item

Gas

Description

EcrecoverGas

3000

Perform ECRecover operaton

Sha256BaseGas

60

Perform sha256 hash operation

Sha256PerWordGas

12

​

Ripemd160BaseGas

600

Perform Ripemd160 operation

Ripemd160PerWordGas

120

​

IdentityBaseGas

15

​

IdentityPerWordGas

3

​

ModExpQuadCoeffDiv

20

​

Bn256AddGas

500

Perform Bn256 elliptic curve operation

Bn256ScalarMulGas

40000

​

Bn256PairingBaseGas

100000

​

Bn256PairingPerPointGas

80000

​

VMLogBaseGas

100

Write logs to node's log file - Klaytn only

VMLogPerByteGas

20

Klaytn only

FeePayerGas

300

Get feePayer's address - Klaytn only

ValidateSenderGas

5000 per signature

Validate the sender's address and signature - Klaytn only

Total gas of those items which has XXXBaseGas and XXXPerWordGas (e.g. Sha256BaseGas, Sha256PerWordGas) are calcluated as

TotalGas = XXXBaseGas + (number of words * XXXPerWordGas)
ValidateSenderGas have to be paid per signature basis.

TotalGas = number of signatures * ValidateSenderGas
### Account-related Gas Table
Item

Gas

Description

TxAccountCreationGasPerKey

20000

Gas required for a key-pair creation

TxValidationGasPerKey

15000

Gas required for a key validation

TxGasAccountUpdate

21000

Gas required for an account update

TxGasFeeDelegated

10000

Gas required for a fee delegation

TxGasFeeDelegatedWithRatio

15000

Gas required for a fee delegation with ratio

TxGasCancel

21000

Gas required to cancel a transaction which has a same nonce

TxGasValueTransfer

21000

Gas required to transfer KLAY

TxGasContractExecution

21000

Base gas for contract execution

TxDataGas

100

Gas required per transaction's single byte

Gas for payload data is calculated as below

GasPayload = number_of_bytes * TxDataGas
### Gas Formula for Transaction Types
TxType

Gas

LegacyTransaction

TxGas + PayloadGas + KeyValidationGas

ValueTransfer

TxGasValueTransfer + KeyValidationGas

ValueTransferMemo

TxGasValueTransfer + PayloadGas + KeyValidationGas

AccountUpdate

TxGasAccountUpdate + KeyCreationGas + KeyValidationGas

SmartContractDeploy

TxGasContractCreation + PayloadGas + KeyValidationGas

SmartContractExecution

TxGasContractExecution + PayloadGas + KeyValidationGas

Cancel

TxGasCancel + KeyValidationGas

KeyValidationGas is defined as below based on key type,

Key Type

Gas

Nil

N/A

Legacy

0

Fail

0

Public

0

MultiSig

(keys-1) * GasValidationPerKey (15000)

RoleBased

Based on keys in the role used in the validation

KeyCreationGas is defined as below based on key type,

Key Type

Gas

Nil

N/A

Legacy

0

Fail

0

Public

GasCreationPerKey (20000)

MultiSig

(keys) * GasCreationPerKey

RoleBased

Gas fee calculated based on keys in each role.
e.g., GasRoleTransaction = (keys)  GasCreationPerKey
GasRoleAccountUpdate = (keys)  GasCreationPerKey
GasRoleFeePayer = (keys) * GasCreationPerKey
