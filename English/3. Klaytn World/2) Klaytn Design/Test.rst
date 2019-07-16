Roles
=====

Roles of AccountKeyRoleBased are defined as below:
--------------------------------------------------

Role

Description

RoleTransaction

Index 0. Default key. Transactions other than TxTypeAccountUpdate should be signed by the key of this role.

RoleAccountUpdate

Index 1. TxTypeAccountUpdate transaction should be signed by this key. If this key is not present in the account, TxTypeAccountUpdate transaction is validated using RoleTransaction key.

RoleFeePayer

Index 2. If this account wants to send tx fee instead of the sender, the transaction should be signed by this key.  If this key is not present in the account, a fee-delegated transaction is validated using RoleTransaction key.

### RLP Encoding
0x05 + encode([key1, key2, key3])

Note that key1, key2, and key3 can be any of above keys (AccountKeyNil, AccountKeyLegacy, AccountKeyPublic, AccountKeyFail, and AccountKeyWeightedMultiSig).

### Omissible and Extendable Roles
The roles can be omitted from the last, and the omitted roles are mapped to the first role. However, a role in the middle cannot be omitted, which means RoleTransaction and RoleFeePayer cannot be set without RoleAccountUpdate. For example, if a role-based key is set to 0x05 + encode([key1, key2]), RoleFeePayer works as if the key is set like 0x05 + encode([key1, key2, key1]).

This feature is provided to extend more roles in the future. If a new role is provided, the new role of accounts already created with old roles is mapped to the first role.

### RLP Encoding (Example)
RoleTransaction Key
PubkeyX 0xe4a01407460c1c03ac0c82fd84f303a699b210c0b054f4aff72ff7dcdf01512d
PubkeyY 0x0a5735a23ce1654b14680054a993441eae7c261983a56f8e0da61280758b5919
RoleAccountUpdate Key
Threshold: 2
Key0 Weight:1
PubkeyX 0xe4a01407460c1c03ac0c82fd84f303a699b210c0b054f4aff72ff7dcdf01512d
PubkeyY 0x0a5735a23ce1654b14680054a993441eae7c261983a56f8e0da61280758b5919
Key1 Weight:1
PubkeyX 0x36f6355f5b532c3c1606f18fa2be7a16ae200c5159c8031dd25bfa389a4c9c06
PubkeyY 0x6fdf9fc87a16ac359e66d9761445d5ccbb417fb7757a3f5209d713824596a50d
RoleFeePayer Key
PubkeyX 0xc8785266510368d9372badd4c7f4a94b692e82ba74e0b5e26b34558b0f081447
PubkeyY 0x94c27901465af0a703859ab47f8ae17e54aaba453b7cde5a6a9e4a32d45d72b2
​
