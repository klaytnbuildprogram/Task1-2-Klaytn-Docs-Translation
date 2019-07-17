# Klaystagram

## Table of Contents
​1. Environment Setup​

​2. Clone Klaystagram BApp​

​3. Directory Structure​

​4. Write Klaystagram Smart Contract​

​5. Deploy Contract​

​6. Frontend Code Overview​

​7. FeedPage​

​7-1. Connect Contract to Frontend​

​7-2. UploadPhoto Component​

​7-3. Feed Component​

​7-4. TransferOwnership Component​

​8. Run App​

## Introduction
​​Klaystagram Introduction Video​​

In this tutorial, we will learn how to make Klaystagram, a Klaytn-based NFT photo licensing application. This simple web application requires basic knowledge of Solidity, JavaScript and React.

NFT refers to a non-fungible token, which is a special type of token that represents a unique asset. As the name non-fungible implies, every single token is unique. And this uniqueness of NFT opens up new horizons of asset digitization. For example, it can be used to represent digital art, game items, or any kind of unique assets and allow people to trade them. For more information, refer to this article.

In Klaystagram, every token represents users' unique pictures. When a user uploads a photo, a unique token is created containing the image data and its ownership. All transactions are recorded on the blockchain, so even service providers do not have control over the uploaded photos. Considering the purpose of this tutorial, only core functions will be implemented. After finishing this tutorial, try adding some more cool features and make your own creative service.

There are three main features.

Photo upload
Users can upload photos along with descriptions on the Klaytn blockchain. The photos will be tokenized.

Feed
Users can see all the photos uploaded on the blockchain.

Transfer ownership
The owner of the photo can transfer ownership of the photo to another user, and the transaction will be shown in the ownership history.

Klaystagram Full Code
https://github.com/underbleu/klaystagram​

## Intended Audience
We will build a web application that interacts with smart contracts. To complete this tutorial, the audience is expected to be familiar with the following concepts.

Basic knowledge on React and Redux. This course is not for absolute beginners.

Basic knowledge and experience in Solidity development are recommended. However, any experienced SW developer should be able to complete the task by following the step-by-step guideline of this tutorial.

Anyone interested in ERC-721 Tokens.

## Testing Environment
Klaystagram BApp is tested in the following environment.

MacOS Mojave 10.14.5

Node 10.16.0 (LTS)

Python 2.7.10
