---
layout: post
title: UTXO and Assignment1
date: 2017-12-17 21:00:00 +0530
---

For those who are taking the [Crypto course](https://www.coursera.org/learn/cryptocurrency/home/welcome) and have met [assignment1](https://www.coursera.org/learn/cryptocurrency/programming/KOo3V/scrooge-coin), you'd agree that it isn't the most well explained for someone who is noob in bitcoin and crypto. Athough the video content has been good, the assignment requires understanding of few terms that were not discussed in the videos. This post covers those terms and help you get started.

**Txn Output** in a transaction tells you *how much* money is being paid and to *whom* it is being paid. 

**Txn Input** in a transaction tells *which coins* we are going to use up (and *who* owns them, and whether or not this is an authentic request by the owner). 

**UTXO** stands for "*unspent* transaction output". It's literally a Txn Output which has NOT been used as an input in some other transaction. That's it. And yeah, a group of UTXOs is collectively called a **UTXOPool** (wow, genius).

![Input coming from UTXOPool and Outputs going back to UTXOPool](https://user-images.githubusercontent.com/6178383/34082264-f18c526e-e380-11e7-9580-bf6a97ca74e3.jpg)


We know that the 'coins' of the currency are *immutable*. We don't simply change the ownership of a coin from sender to receiver as part of a transaction. When a transaction takes place, Inputs are deleted and Outputs are created as new UTXO (and go in the UTXOPool) that may then be consumed in future transactions.


*Well, thanks for the info. But I still don't no where to start! :(*  
I'll try to expand on the comments that are part of the assignment. That's all I can do if I want to honour the Honor Code. :P

```
 * @return true if: 
 *(1) all outputs claimed by {@code tx} are in the current UTXO pool
```
The Inputs for the transaction we are validating should be in UTXOPool
```
 *(2) the signatures on each input of {@code tx} are valid,
```
Each Input should be verified using the public key(which is same as the recepient's _address_)
```
*(3) no UTXO is claimed multiple times by {@code tx}, 
```
We should be careful that Tx1 and Tx2 in the pic above, should not be same.
```
*(4) all of {@code tx}s output values are non-negative,
```
We can't transfer a Rs -1 million :P
```
 * (5) the sum of {@code tx}s input values is greater than 
 * or equal to the sum of its output values; and false otherwise.
```
The total value of the Input value should be greater than equal to the output value. 

If you are wondering why isn't the Input value and the Output value required to be same in the last comment? Well, technically it will be. That difference `OutputSum - InputSum` is called the **Txn Change**. It usually goes back to the sender (as change amount, like you get back from the cashier when you pay a dollar for something worth 99 cents) or charged as a txn fee.


