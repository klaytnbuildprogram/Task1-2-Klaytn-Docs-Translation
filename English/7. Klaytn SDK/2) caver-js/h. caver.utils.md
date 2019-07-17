# caver.utils

caver.utils provides utility functions.

## randomHex
caver.utils.randomHex(size)
The randomHex library to generate cryptographically strong pseudo-random HEX strings from a given byte size.

Parameters

Name

Type

Description

size

Number

The byte size for the HEX string, e.g., 32 will result in a 32-byte HEX string with 64 characters preficed with "0x".

Return Value

Type

Description

String

The generated random HEX string.

Example

> caver.utils.randomHex(32);
"0xa5b9d60f32436310afebcfda832817a68921beb782fabf7915cc0460b443116a"
​
> caver.utils.randomHex(4);
"0x6892ffc6"
​
> caver.utils.randomHex(2);
"0x99d6"
​
> caver.utils.randomHex(1);
"0x9a"
​
> caver.utils.randomHex(0);
"0x"
_
caver.utils._()
The underscore library for many convenience JavaScript functions.

See the underscore API reference for details.

Example

> var _ = caver.utils._;
​
> _.union([1,2],[3]);
[1,2,3]
​
> _.each({my: 'object'}, function(value, key){ ... });
...
## BN
caver.utils.BN(mixed)
The BN.js library for calculating with big numbers in JavaScript. See the BN.js documentation for details.

Parameters

Name

Type

Description

mixed

String | Number

A number, number string or HEX string to convert to a BN object.

Return Value

Type

Description

Object

The BN.js instance.

Example

> var BN = caver.utils.BN;
​
> new BN(1234).toString();
"1234"
​
> new BN('1234').add(new BN('1')).toString();
"1235"
​
> new BN('0xea').toString();
"234"
## isBN
caver.utils.isBN(bn)
Checks if a given value is a BN.js instance.

Parameters

Name

Type

Description

bn

Object

A BN.js instance.

Return Value

Type

Description

Boolean

true if a given value is a BN.js instance.

Example

> var number = new BN(10);
> caver.utils.isBN(number);
true
## isBigNumber
caver.utils.isBigNumber(bignumber)
Checks if a given value is a BigNumber.js instance.

Parameters

Name

Type

Description

bignumber

Object

A BigNumber.js instance.

Return Value

Type

Description

Boolean

true if a given value is a BigNumber.js instance.

Example

> var number = new BigNumber(10);
> caver.utils.isBigNumber(number);
true
## sha3
caver.utils.sha3(string)
caver.utils.keccak256(string) // ALIAS
Calculates the sha3 of the input.

NOTE: To mimic the sha3 behavior of Solidity use caver.utils.soliditySha3.

Parameters

Name

Type

Description

string

String

A string to hash.

Return Value

Type

Description

String

The result hash.

Example

> caver.utils.sha3('234'); // taken as string
"0xc1912fee45d61c87cc5ea59dae311904cd86b84fee17cc96966216f811ce6a79"
​
> caver.utils.sha3(new BN('234')); // utils.sha3 stringify bignumber instance.
"0xc1912fee45d61c87cc5ea59dae311904cd86b84fee17cc96966216f811ce6a79"
​
> caver.utils.sha3(234);
null // can't calculate the has of a number
​
> caver.utils.sha3(0xea); // same as above, just the HEX representation of the number
null
​
> caver.utils.sha3('0xea'); // will be converted to a byte array first, and then hashed
"0x2f20677459120677484f7104c76deb6846a2c071f9b3152c103bb12cd54d1a4a"
## soliditySha3
caver.utils.soliditySha3(param1 [, param2, ...])
Calculates the sha3 of given input parameters in the same way solidity would. This means arguments will be ABI converted and tightly packed before being hashed.

Parameters

Name

Type

Description

​

​

​

​

​

paramX

Mixed

Any type, or an object with {type: 'uint', value: '123456'} or {t: 'bytes', v: '0xfff456'}. Basic types are autodetected as follows:
 - String non numerical UTF-8 string is interpreted as string.
 - ``String

Number

BN

HEXpositive number is interpreted asuint256.<br> -String

Number

BNnegative number is interpreted asint256.<br> -Booleanasbool.<br> -StringHEX string with leading0xis interpreted asbytes.<br> -HEXHEX number representation is interpreted asuint256``.


Return Value

Type

Description

String

The result hash.

Example

> caver.utils.soliditySha3('234564535', '0xfff23243', true, -10);
// auto detects: uint256, bytes, bool, int256
"0x3e27a893dc40ef8a7f0841d96639de2f58a132be5ae466d40087a2cfa83b7179"
​
> caver.utils.soliditySha3('Hello!%'); // auto detects: string
"0x661136a4267dba9ccdf6bfddb7c00e714de936674c4bdb065a531cf1cb15c7fc"
​
> caver.utils.soliditySha3('234'); // auto detects: uint256
"0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"
​
> caver.utils.soliditySha3(0xea); // same as above
"0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"
​
> caver.utils.soliditySha3(new BN('234')); // same as above
"0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"
​
> caver.utils.soliditySha3({type: 'uint256', value: '234'})); // same as above
"0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"
​
> caver.utils.soliditySha3({t: 'uint', v: new BN('234')})); // same as above
"0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"
​
> caver.utils.soliditySha3('0x407D73d8a49eeb85D32Cf465507dd71d507100c1');
"0x4e8ebbefa452077428f93c9520d3edd60594ff452a29ac7d2ccc11d47f3ab95b"
​
> caver.utils.soliditySha3({t: 'bytes', v: '0x407D73d8a49eeb85D32Cf465507dd71d507100c1'});
"0x4e8ebbefa452077428f93c9520d3edd60594ff452a29ac7d2ccc11d47f3ab95b" // same result as above
​
> caver.utils.soliditySha3({t: 'address', v: '0x407D73d8a49eeb85D32Cf465507dd71d507100c1'});
"0x4e8ebbefa452077428f93c9520d3edd60594ff452a29ac7d2ccc11d47f3ab95b" // same as above, but will do a checksum check, if its multi case
​
> caver.utils.soliditySha3({t: 'bytes32', v: '0x407D73d8a49eeb85D32Cf465507dd71d507100c1'});
"0x3c69a194aaf415ba5d6afca734660d0a3d45acdc05d54cd1ca89a8988e7625b4" // different result as above
​
> caver.utils.soliditySha3({t: 'string', v: 'Hello!%'}, {t: 'int8', v:-23}, {t: 'address', v: '0x85F43D8a49eeB85d32Cf465507DD71d507100C1d'});
"0xa13b31627c1ed7aaded5aecec71baf02fe123797fffd45e662eac8e06fbe4955"
## isHex
caver.utils.isHex(hex)
Checks if a given string is a HEX string.

Parameters

Name

Type

Description

hex

String | HEX

The given HEX string.

Return Value

Type

Description

Boolean

true if a given string is a HEX string.

Example

> caver.utils.isHex('0xc1912');
true
​
> caver.utils.isHex(0xc1912);
true
​
> caver.utils.isHex('c1912');
true
​
> caver.utils.isHex(345);
true // this is tricky, as 345 can be a HEX representation or a number, be careful when not having a 0x in front!
​
> caver.utils.isHex('0xZ1912');
false
​
> caver.utils.isHex('Hello');
false
## isHexStrict
caver.utils.isHexStrict(hex)
Checks if a given string is a HEX string. Difference to caver.utils.isHex is that it expects HEX to be prefixed with 0x.

Parameters

Name

Type

Description

hex

String | HEX

The given HEX string.

Return Value

Type

Description

Boolean

true if a given string is a HEX string.

Example

> caver.utils.isHexStrict('0xc1912');
true
​
> caver.utils.isHexStrict(0xc1912);
false
​
> caver.utils.isHexStrict('c1912');
false
​
> caver.utils.isHexStrict(345);
false // this is tricky, as 345 can be a HEX representation or a number, be careful when not having a 0x in front!
​
> caver.utils.isHexStrict('0xZ1912');
false
​
> caver.utils.isHex('Hello');
false
## isAddress
caver.utils.isAddress(address)
Checks if a given string is a valid Klaytn address. It will also check the checksum, if the address has upper and lowercase letters.

Parameters

Name

Type

Description

address

String

An address string.

Return Value

Type

Description

Boolean

true if a given string is a valid Klaytn address.

Examples

> caver.utils.isAddress('0xc1912fee45d61c87cc5ea59dae31190fffff232d');
true
​
> caver.utils.isAddress('c1912fee45d61c87cc5ea59dae31190fffff232d');
true
​
> caver.utils.isAddress('0XC1912FEE45D61C87CC5EA59DAE31190FFFFF232D');
true // as all is uppercase, no checksum will be checked
​
> caver.utils.isAddress('0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d');
true
​
> caver.utils.isAddress('0xC1912fEE45d61C87Cc5EA59DaE31190FFFFf232d');
false // wrong checksum
## toChecksumAddress
caver.utils.toChecksumAddress(address)
Converts an upper or lowercase Klaytn address to a checksum address.

Parameters

Name

Type

Description

address

String

An address string.

Return Value

Type

Description

String

The checksum address.

Examples

> caver.utils.toChecksumAddress('0xc1912fee45d61c87cc5ea59dae31190fffff232d');
"0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d"
​
> caver.utils.toChecksumAddress('0XC1912FEE45D61C87CC5EA59DAE31190FFFFF232D');
"0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d" // same as above
## checkAddressChecksum
caver.utils.checkAddressChecksum(address)
Checks the checksum of a given address. Will also return false on non-checksum addresses.

Parameters

Name

Type

Description

address

String

An address string.

Return Value

Type

Description

Boolean

true when the checksum of the address is valid, false if it is not a checksum address, or the checksum is invalid.

Examples

> caver.utils.checkAddressChecksum('0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d');
true
## toHex
caver.utils.toHex(mixed)
Converts any given value to HEX. Number strings will interpreted as numbers. Text strings will be interpreted as UTF-8 strings.

Parameters

Name

Type

Description

mixed

String | Number | BN | BigNumber

The input to convert to HEX.

Return Value

Type

Description

String

The resulting HEX string.

Examples

> caver.utils.toHex('234');
"0xea"
​
> caver.utils.toHex(234);
"0xea"
​
> caver.utils.toHex(new BN('234'));
"0xea"
​
> caver.utils.toHex(new BigNumber('234'));
"0xea"
​
> caver.utils.toHex('I have 100€');
"0x49206861766520313030e282ac"
## toBN
caver.utils.toBN(number)
Safely converts any given value (including BigNumber.js instances) into a BN.js instance, for handling big numbers in JavaScript.

NOTE: For just the BN.js class, use caver.utils.BN.

Parameters

Name

Type

Description

number

String | Number | HEX

Number to convert to a big number.

Return Value

Type

Description

Object

The BN.js instance.

Examples

> caver.utils.toBN(1234).toString();
"1234"
​
> caver.utils.toBN('1234').add(caver.utils.toBN('1')).toString();
"1235"
​
> caver.utils.toBN('0xea').toString();
"234"
## hexToNumberString
caver.utils.hexToNumberString(hex)
Returns the number representation of a given HEX value as a string.

Parameters

Name

Type

Description

hexString

HEX String

A HEX string to be converted.

Return Value

Type

Description

String

The number as a string.

Examples

> caver.utils.hexToNumberString('0xea');
"234"
## hexToNumber
caver.utils.hexToNumber(hex)
Returns the number representation of a given HEX value.

NOTE: This is not useful for big numbers, rather use caver.utils.toBN.

Parameters

Name

Type

Description

hexString

HEX String

A HEX string to be converted.

Return Value

Type

Description

Number

The number representation of a given HEX value.

Examples

> caver.utils.hexToNumber('0xea');
234
## numberToHex
caver.utils.numberToHex(number)
Returns the HEX representation of a given number value.

Parameters

Name

Type

Description

number

String | Number | BN | BigNumber

A number as string or number.

Return Value

Type

Description

String

The HEX value of the given number.

Examples

> caver.utils.numberToHex('234');
'0xea'
## hexToUtf8
caver.utils.hexToUtf8(hex)
caver.utils.hexToString(hex) // ALIAS
Returns the UTF-8 string representation of a given HEX value.

Parameters

Name

Type

Description

hex

String

A HEX string to convert to a UTF-8 string.

Return Value

Type

Description

String

The UTF-8 string.

Examples

> caver.utils.hexToUtf8('0x49206861766520313030e282ac');
"I have 100€"
## hexToAscii
caver.utils.hexToAscii(hex)
Returns the ASCII string representation of a given HEX value.

Parameters

Name

Type

Description

hex

String

A HEX string to convert to a ASCII string.

Return Value

Type

Description

String

The ASCII string.

Examples

> caver.utils.hexToAscii('0x4920686176652031303021');
"I have 100!"
## utf8ToHex
caver.utils.utf8ToHex(string)
caver.utils.stringToHex(string) // ALIAS
Returns the HEX representation of a given UTF-8 string.

Parameters

Name

Type

Description

string

String

A UTF-8 string to convert to a HEX string.

Return Value

Type

Description

String

The HEX string.

Examples

> caver.utils.utf8ToHex('I have 100€');
"0x49206861766520313030e282ac"
## asciiToHex
caver.utils.asciiToHex(string)
Returns the HEX representation of a given ASCII string.

Parameters

Name

Type

Description

string

String

An ASCII string to convert to a HEX string.

Return Value

Type

Description

String

The HEX string.

Examples

> caver.utils.asciiToHex('I have 100!');
"0x4920686176652031303021"
## hexToBytes
caver.utils.hexToBytes(hex)
Returns a byte array from the given HEX string.

Parameters

Name

Type

Description

hex

HEX String

A HEX string to be converted.

Return Value

Type

Description

Array

The byte array.

Examples

> caver.utils.hexToBytes('0x000000ea');
[ 0, 0, 0, 234 ]
## bytesToHex
caver.utils.bytesToHex(byteArray)
Returns a HEX string from a byte array.

Parameters

Name

Type

Description

byteArray

Array

A byte array to convert.

Return Value

Type

Description

String

The HEX string.

Examples

> caver.utils.bytesToHex([ 72, 101, 108, 108, 111, 33, 36 ]);
"0x48656c6c6f2125"
## toPeb
caver.utils.toPeb(number [, unit])
Converts any KLAY value into peb.

NOTE: "peb" is the smallest KLAY unit, and you should always make calculations in peb and convert only for display reasons.

Parameters

Name

Type

Description

number

String | Number | BN

The value.

unit

String

(optional, defaults to "KLAY") KLAY to convert from. Possible units are:
- peb: '1' 
 - kpeb: '1000' 
 - Mpeb: '1000000' 
 - Gpeb: '1000000000' 
 - Ston: '1000000000' 
 - uKLAY: '1000000000000' 
 - mKLAY: '1000000000000000' 
 - KLAY: '1000000000000000000' 
 - kKLAY: '1000000000000000000000' 
 - MKLAY: '1000000000000000000000000' 
 - GKLAY: '1000000000000000000000000000' 


Return Value

Type

Description

String | BN

If a number or a string is given, it returns a number string, otherwise a BN.js instance.

Examples

> caver.utils.toPeb('1', 'KLAY');
"1000000000000000000"
## fromPeb
caver.utils.fromPeb(number [, unit])
NOTE: "peb" is the smallest KLAY unit, and you should always make calculations in KLAY and convert only for display reasons.

Parameters

Name

Type

Description

number

String | Number | BN

The value in peb.

unit

String

(optional, defaults to "KLAY") KLAY to convert to. Possible units are:
- peb: '1' 
 - kpeb: '1000' 
 - Mpeb: '1000000' 
 - Gpeb: '1000000000' 
 - Ston: '1000000000' 
 - uKLAY: '1000000000000' 
 - mKLAY: '1000000000000000' 
 - KLAY: '1000000000000000000' 
 - kKLAY: '1000000000000000000000' 
 - MKLAY: '1000000000000000000000000' 
 - GKLAY: '1000000000000000000000000000' 


Return Value

Type

Description

String | BN

If a number or a string is given, it returns a number string, otherwise a BN.js instance.

Examples

> caver.utils.fromPeb('1', 'KLAY');
"0.000000000000000001"
## unitMap
caver.utils.unitMap
Shows all possible KLAY values and their amount in peb.

Return Value

Type

Description

Object

With the following properties:
- peb: '1' 
 - kpeb: '1000' 
 - Mpeb: '1000000' 
 - Gpeb: '1000000000' 
 - Ston: '1000000000' 
 - uKLAY: '1000000000000' 
 - mKLAY: '1000000000000000' 
 - KLAY: '1000000000000000000' 
 - kKLAY: '1000000000000000000000' 
 - MKLAY: '1000000000000000000000000' 
 - GKLAY: '1000000000000000000000000000' 


Examples

> caver.utils.unitMap
​
​
{
  peb: '1',
  kpeb: '1000',
  Mpeb: '1000000',
  Gpeb: '1000000000',
  Ston: '1000000000',
  uKLAY: '1000000000000',
  mKLAY: '1000000000000000',
  KLAY: '1000000000000000000',
  kKLAY: '1000000000000000000000',
  MKLAY: '1000000000000000000000000',
  GKLAY: '1000000000000000000000000000',
}
## padLeft
caver.utils.padLeft(string, characterAmount [, sign])
caver.utils.leftPad(string, characterAmount [, sign]) // ALIAS
Adds a padding on the left of a string. Useful for adding paddings to HEX strings.

Parameters

Name

Type

Description

string

String

The string to add padding on the left.

characterAmount

Number

The number of characters the total string should have.

sign

String

(optional) The character sign to use, defaults to "0".

Return Value

Type

Description

String

The padded string.

Examples

> caver.utils.padLeft('0x3456ff', 20);
"0x000000000000003456ff"
​
> caver.utils.padLeft(0x3456ff, 20);
"0x000000000000003456ff"
​
> caver.utils.padLeft('Hello', 20, 'x');
"xxxxxxxxxxxxxxxHello"
## padRight
caver.utils.padRight(string, characterAmount [, sign])
caver.utils.rightPad(string, characterAmount [, sign]) // ALIAS
Adds a padding on the right of a string, Useful for adding paddings to HEX strings.

Parameters

Name

Type

Description

string

String

The string to add padding on the right.

characterAmount

Number

The number of characters the total string should have.

sign

String

(optional) The character sign to use, defaults to "0".

Return Value

Type

Description

String

The padded string.

Examples

> caver.utils.padRight('0x3456ff', 20);
"0x3456ff00000000000000"
​
> caver.utils.padRight(0x3456ff, 20);
"0x3456ff00000000000000"
​
> caver.utils.padRight('Hello', 20, 'x');
"Helloxxxxxxxxxxxxxxx"
## toTwosComplement
caver.utils.toTwosComplement(number)
Converts a negative numer into a two's complement.

Parameters

Name

Type

Description

number

Number | String | BigNumber

The number to convert.

Return Value

Type

Description

String

The converted hex string.

Examples

> caver.utils.toTwosComplement('-1');
"0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
​
> caver.utils.toTwosComplement(-1);
"0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
​
> caver.utils.toTwosComplement('0x1');
"0x0000000000000000000000000000000000000000000000000000000000000001"
​
> caver.utils.toTwosComplement(-15);
"0xfffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff1"
​
> caver.utils.toTwosComplement('-0x1');
"0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
