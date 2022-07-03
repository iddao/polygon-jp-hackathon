# Polygon Tokyo Hack Submission Repository

This is a meta-repository of my work on Polygon Tokyo Hack.

## Project Name

ID DAO

## About this project

On-chain KYC Protocol

Complete KYC on chain with your national ID card while maintaining privacy.
Your ID card also become hardware wallet.

## The problem it is solving

- Money laundering on DEX
    - With this, DEX contract itself can easily prevent malicious transaction.
- Traditional KYC Cost
    - Maintaining KYC system is expensive
- Privacy
    - Users need to give their name, address, selfie, etc during KYC.
- Identity Oracle
    - Bonding an account and traditional family registry needs some sort of oracle.
    - These oracle should be sound.
    - This brings family registry to blockchain as an oracle.

## Technology used

### ISO 7816, ISO 14443 

aka Smart card/NFC.

Used for reading national ID card. Currently Japanese "my number" Card is supported. In the future other cards will be supported.

Install app, touch the card to smartphone, get connected.

### WalletConnect

You can connect your card to Dapps with WalletConnect.

Also, I used this for sharing signature.
By this, non-blockchain apps such as [マイナポータル](https://myna.go.jp) can be integrated as a way of linking.
App developers don't need to create new app only for reading the card anymore

### RSA Digital Signature

The contract verifies RSA signature provided by user and proves the user's action.
The contract also verifies RSA signature provided by government and proves the user is authorized by government.

Now it supports Japanese "my number" card, and Japanese Public Key Infrastructure(JPKI), which is authority of my number card.
ID DAO can support any RSA compatible signer in theory.

### EIP-198: Big integer modular exponentiation

https://eips.ethereum.org/EIPS/eip-198

EIP-198 is the EIP that make it easier to compute modular exponentiation.
This precompiled contract solves it with each variable can have arbitrary size of integer. 

$${b}^{e}\mod m (b,e,m \in \mathbb{N}) $$

By this, the contract can verify RSA signature cheap.
