
# Bitwise Operations


## Unsign Bit

All positive

## Sign Bit

Has positive + negative

## Binary

```text
00000001 = 1
00000010 = 2
```


## Swift


You need to have `Ob` as a suffix to denote the binary
```swift
let byteValue1: UInt8 = 0b00000001
print(byteValue1)
```


### Inverse

```swift
//Bitwise Not Operator
let bitwiseNotByte: UInt8 = 0b00001111
~bitwiseNotByte     // equals 11110000

//Bitwise AND Operator
let bitwiseAndByte: UInt8 = 0b11000000
let bitwiseAndMask: UInt8 = 0b11111111
let bitwiseAndResult = bitwiseAndByte & bitwiseAndMask 
                    // equals 11000000

//Bitwise OR Operator
let bitwiseOrByte: UInt8 = 0b10110010
let bitwiseOrMask: UInt8 = 0b01011110
let bitwiseOrResult = bitwiseOrByte | bitwiseOrMask 
                   // equals 11111110

//Bitwise XOR Operator
let bitwiseXorByte: UInt8 = 0b00010100
let bitwiseXorMask: UInt8 = 0600000101
let bitwiseXoResult = bitwiseXorByte ^ bitwiseXorMask 
                    // equals 00010001
```


## Decoding Base 64



## Mind Map

[logic_gates](logic_gates.md)