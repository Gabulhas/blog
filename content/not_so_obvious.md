---
title: "Not so obvious - Blockchain related stuff you can't easily find online"
date: 2023-06-03T9:55:33+01:00
draft: false
---


These topics arise from the fact that they hard to find the explanation online, or the explanation online is the most generic garbage and you don't understand the details. For example, if you search online "what's Bitcoin Mining", most explanations online just mention that "mining is the computation of a mathematical problem", or "computers compete to be the first one to solve a puzzle", but what actually happens? Why does even exist? Why do you have to tell me your whole life history for me to understand this?

So the point of this post is to be some sort of FAQ for stuff you can't really find the explanation online.

# How does mining actually works and why it exists

I will actually start by answering the question of "Why does mining exist?".

## Why does it exist

Ever wondered what **Decentralized** and **Permissionless** mean? Decentralized means that there's no single authority that rules over the network, and Permissionless means that everyone has permission to participate in the network (to validate transactions, blocks, etc), where as Permissioned means that only a set of entities can participate.

Ever wondered how Bitcoin (and other Proof of Work networks) achieve Decentralization in a Permissionless manner?
If you really think about it, how can you have a system that everyone can change something (the ledger), everyone can participate (say that a transaction is valid, that the state is valid) and then can share their views with no rules!
Also, how can we achieve a consensus of the new state, that is, how can we together, in a democratic kind of way, manage to decide what changes should be made (what transactions should be added) and if the changes that were made were valid?
How can we EVEN DO THIS IF ANYONE CAN MAKE NEW "ACCOUNTS"/KEYS!??!
This is the problem that Bitcoin solved.

Mining exists so there's a way to reach consensus in these settings. Instead of each person having a single vote (that would be democratic), we have mining, because is not possible to tell if a person is acting like multiple people (Sybil attacks), since you can just create as many "accounts" (public keys) as you want in your PC. So the Democratic/Per Person Vote is changed with this concept of "Mining Power" or "Proofs of Work", where instead of voting, there's a probabilistic chance, depending on the amount of mining power, that a participant (a Node, you can think about it as a person) can successfully mine a block and have a say in how the block is formed (within predefined rules).

The rest of the network still validates and either accepts or denies blocks coming from the network, so there's still validation besides the node that mines. Validation involves checking if the transactions are possible (if someone has enough money to transfer), if the structure of the block is correct and if the proof of the mining is valid (I will explain this later).

So it exists to replace the concept of Voting with the concept of Mining Power.

## How does it actually work
I'm assuming that you know what an hash function. This is the concept that is actually readily available online ([Hash Function](https://en.wikipedia.org/wiki/Hash_function)).

The proprety that is important here is the fact that you can't reverse compute an hash, that is, you can't calculate the value of something from the hash, nor there's a way to achieve a value from an hash, and that's what is important. You can only know the hash value of something if you actually execute the function, and you don't know before hand what will the hash value "look" like. This propriety can be used to make some sort of "lottery" in a decentralized/offline sense.

So the puzzle here is just a value that, when hashed, it results in a hash value with specific characteristics. What we want to know is which value makes a hash with those characteristics.

The puzzle in Bitcoin involves computing a nonce (basically, a just number) that meets certain conditions, as outlined by the equation H(hi−1,nonce,tx,par) < Target, where
- "hi−1" is the hash of the previous block
- "tx" represents the set of validated transaction's
- "par" represents other parameters such as blockchain version and cryptographic parameters.
- "Target" is a value decided by the network that means "how hard is to find the next puzzle".

Mathsy stuff aside, the mining is just this:

The node has a block already built, with a header formed (containing the hash to the previous block, and a Merkle Tree/Fingerprint of the transactions included), but there's a special space/section in the block header, that will contain the number.

What the node will then do is, it will try every possible number for a nonce (just guess work, randomly trying every number) and hashing the resulting header (with the number it's trying) until one of the hashes has a value lower than the value "Target", which is basically the difficulty decided by the network (don't think much about this now, is just a value, we will discuss it later).

And by "lower" I mean "finding a number that will make the hash contain X zeros as a prefix" (not necessarily, but that is what happens most of the time).


Look at this [block](https://www.blockchain.com/explorer/blocks/btc/815891): You will see that it's Hash is actually "**0000000000000000000**1a9288ef75a04adaab35e6006e81dfae56eae3d3ea085", and it's nonce is "771177056". So a computer had to build the block (basically just had to put transactions in it, and some other stuff), and had to try every possibility, from 0 to the "nonce" value, until it found that the hash of the block containing that nonce was lower than the expected difficulty. While this was happening, a ton of other computers were also trying the same.

The block creator was the lucky lottery winner.

(Note that sometimes, multiple computers find a block in relatively similar times. The block that spreads faster/has more blocks appended to it is the considered winner.)

**That is mining.**

## How do proofs of work result in a "democratic" vote
Even thought that is not democratic, it's pretty close (at least in practice and how it was imagined).

So the more processing power a node has, the more tries per second for a nonce it can do which results in a higher chance of being the first to "mine" the block. We should assume that most of the network is fair and participating in a non-malicious way.
If more than 50% (that's where the 51% comes from) of the processing power of the networks belong to malicious entities, then those entities can act in a malicious way, since most of the blocks will be mined by them.


# How does Bitcoin enforces a 10min Blocktime/The Mechanics of Difficulty Adjustment in Blockchain
Ever wondered how does Bitcoin achieve 10min blocktime? What is there to prevent a node to mine and broadcast a block after just a few seconds? How does everyone reach an agreement together if everyone participates independently and without trusting each other?


These kinds of network work on the basis of "If what I receive is wrong, I just wan't accept it", and if everyone does this (independently), the network runs correctly.


Well, you would say "how about using some timestamp that is added to the header, and we check if the incoming blocks actually had to wait 10min to be broadcasted?". What if I told you that

