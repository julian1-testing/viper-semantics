# Semantics of Viper in K

## Viper Language

Viper is a new experimental language in the smart contract domain. It is designed by Ethereum foundation, supposedly being simpler and more secure language than Solidity by factoring out the essential components in writing smart contracts, based on their experience of deploying and operating hundreds of thousands of smart contracts over the last two years.

Specifically, Viper is an object-oriented language; a smart contract is represented as a class where the data fields hold the contract status and the methods provides the contract functionalities. Notably, however, it has no explicit inheritance --- one of the main design decision made based on their extensive experience of writing smart contracts. They found that security is more important than programming convenience, thus the minimality has obvious advantages.

It has simple types: primitive types (`num` of 128-bits signed integer with arithmetic overflow, `decimal` with 128-bits of integer numbers and 10-bits of fractional numbers, `bool`, `address` of 20-bytes, and `bytes32`), and compound types (fixed size of arrays, structs, and maps with primitive type keys).

A local variable has the function scope (i.e., no variable hiding in local blocks) but no declaration is needed, although it is questionable from the security perspective of the language design. It does not allow recursive functions but only loops with break. It borrows the Python syntax, i.e., white space sensitive.

## Viper Semantics Specification

Specifying Viper language semantics is challenging. As an experimental language, Viper does not have a specification document other than the source code of the compiler to EVM. Also, the language keeps evolving. So, we took a snapshot ([a886850c1d](https://github.com/ethereum/viper/tree/a886850c1dbdeb3d63639b0dc5b970bd578b0523)) of the latest compiler source at the moment, and figured out the semantics via reverse-engineering the source code as well as communication with the language designers.

We specified the Viper language semantics by formalizing the translation from Viper to EVM. Viper was designed with the intent of being compiled down to EVM, and thus Viper semantics ended up being closely coupled with EVM semantics. We found that the translation semantics is one of the efficient way of emphasizing the essence of Viper semantics by factoring it out from EVM semantics.

We formalized the translation from Viper to EVM. Our formalization adopted the  two-staged translation approach taken by the Viper compiler, that is, Viper to LLL translation followed by LLL to EVM translation, where LLL is an intermediate representation.

TODO: more details on translation semantics details?

As a side product of formalizing the translation, we found several bugs of Viper compiler, including a critical security vulnerability.

TODO: detailed explanation of the security bug
TODO: brief list of other minor bugs
