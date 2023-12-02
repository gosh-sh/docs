# **Overview**



![](../images/acki_nacki.jpg)

## **Introduction**
*Abstract*



The use cases enabled by GOSH demand so great an amount of data to be processed, that no blockchain technology today can actually cope with handling it entirely on-chain (which, of course, is GOSH’s raison d’etre). We always take as a benchmark the example of the Linux repository; the Linux repository has 50 million objects, ergo 50 million smart contracts. If a user wants to push it onto the blockchain, even if you take at face value what some of the fastest blockchains tell you that they can do (despite the fact that none of it has ever been put into production) it will take 5 hours for the Linux repository to be uploaded. And that is just one user uploading one simple repo. By comparison, they can do this in a few minutes, on a regular basis, with GitHub.

GOSH applications require enabling millions of documents to be processed, and aim to set new standards for work on collaborative projects around a single document, etc. etc. Every aspect of our work requires a tremendous amount of data to be processed on-chain, such that quite simply no blockchain today can do. Ergo we need a new blockchain architecture that will enable us to do what cloud computing can do.

For cloud services, which provide access to databases, and empower high usage applications like GitHub, Microsoft Office, Google Docs, etc. etc. to be stored on the blockchain, there needs to be a decentralized backend that powers these services. We spoke about this for years. We knew that it's coming… And we weren’t ready. Acki Nacki is about solving this problem; a problem of real scalability and finality, in the sense that every user click on the same button on a document, doesn’t require them to wait for minutes…

…Or even for seconds. Research shows that what users actually consider a working state for software is when they wait less than a second for each action. Can we do anything about that? That’s why we created Acki Nacki.



## **Definitions**
*Faster is just a marketing term*


What is faster? Faster is really the amount of data you can process in a particular time frame. So what are you optimized for? The amount of data or the time? Faster is the relation between these two metrics, how many objects are there and how fast each of them is processed. If you're talking about a small object, like deploying a smart contract on a blockchain takes X seconds, is it fast? And if you want a million smart contracts to be deployed, is that considered to be fast? How long should you wait? So there is no real definition of faster. What we need to talk about is the **finality and throughput**. That is: the time the object is deployed, how long it takes for the object or its associated task to be performed, and how many tasks we can perform simultaneously. These two metrics actually intersect. For example, in the TON blockchain you theoretically have a lot of throughput because it can apply states in parallel. You can process many objects at once, yes, but the finality of the TON blockchain is still only about 13 seconds. Or you can have very quick finality in Solana, but the throughput will be limited to simultaneous 2000 transactions. That’s the tradeoff.



## **What Difference Does It Make?**
*The Problem*


Blockchains have different architectures. Of course we're not going to review them all, but we are going to compare them on a given example. There are two major groups of consensus algorithms: Nakamoto consensus and Byzantine Fault Tolerance (BFT) consensus. Nakamoto consensus is probabilistic. The idea is that the longer you build on top of one chain, the more security guarantees you have, with time, and that ultimately your transaction is secure. That's why in Bitcoin, we wait usually between six to 10 blocks to build on top of the chain in which our transaction is included to be sure that any attack on this consensus would have no economic incentive following a certain number of blocks. The amount of electric power you would need in order to mine all of these blocks, include transactions, and withhold them, would be so great that, economically, it's just not possible to assume that someone would be prepared to pay such cost, while actually corrupting the chain would not bring any value in comparison to the price of electricity. That is the main security guarantee of Nakamoto consensus.

BFT consensus, on the other hand, outlines certain assumptions — namely, that if 66% of the validators in the network are honest, and we can guarantee that a transaction is signed by 66% of network participants, it need not afterwards be reviewed or rejected. If you have more than 33% of the network, you can stop the BFT consensus from working entirely, but you will still need 66% to include a malicious transaction. There are some other esoteric algorithms like Algorand (which is marginal and not without its difficulties) and Solana. But Solana also employs BFT on a certain level. And therefore to achieve finality in Solana, with a very low probability of being corrupted, you need to wait 13 blocks. Still four or five seconds. Not fit for purpose.

There are optimizations for BFT, because BFT, like Nakamoto, is a good algorithm; but it's a one chain algorithm, meaning you cannot do sharding, and it still takes a lot of communication. Aptos say they optimize BFT to be about one second. But the problem with that is that even if you can have a finality within a second, it's still one chain. You will not be able to scale this in parallel execution because you will need a lot of these BFTs to work together. And once you have several BFTs working together, then you need a consensus between them, which is what TON attempts to do. The architecture being: A lot of BFT consensuses being regulated by one BFT, which is the master chain, a consensus of consensuses. Which adds another layer of communication and delays finality.

So bottom line, we don't have a single algorithm today that can really guarantee finality under one second, and also support parallel operations. When GOSH talks about consensus algorithms, we use the analogy of it being a processor. For us, the blockchain is really a processor where we run our smart contracts, which are our programs. It's a distributed kind of a processor, all of which today operate like single threaded processors — the [Intel 8086](https://en.wikipedia.org/wiki/Intel_8086) — and blockchains try to make them as rapid as they can. Single thread processors, but really, really fast… The problem with that process is it has the fundamental limitation of still having only one thread, meaning it cannot really execute many operations in parallel. Solana says: “Ok, we have a way around this (kind of). Like a collator, our block proposers will put the blocks inside a huge machine that has many, many physical processors that will execute in parallel.” The first problem with this is you need to put all transaction results into one block, leading to blocks that are simply too large, an issue Vitalik Buterin brought up when announcing Ethereum, stating that Bitcoin blocks are too limited in capacity to sustain a world computer. If you try to perform many operations on a single processor [the communication bus has to be really fat](https://en.wikipedia.org/wiki/Multiple_instruction,_multiple_data). The second problem is that if you have a single threaded machine, you tend actually to create single threaded applications; those with one smart contract like an ERC-20 token, used by millions of people. Imagine, this contract has 20 million users and they try to transfer these tokens between them. It cannot be executed in parallel on time. You'll need to shard this contract somehow to be able to execute it, even in this single thread environment with these many cores in the block proposer’s machine. There’s still a bottleneck. Naturally, certain operations will be split into chunks, because if you want fast finality, you need a block to be released very quickly. And so in order to release blocks very fast, you need to chop off the amount of operations you can perform inside the block, and then get it to another block. So they have a block size of 250 milliseconds. It then moves on to other validators, but you still wait for 5, 6, 7 seconds for finality. The architecture is ok but it's not really what we're looking for when we talk about the ultimate processor. 



## **The Search For The Holy Scale**
*How Acki Nacki Works*


When we talk about a multi-processor, we mean a multi-core, multi-threaded execution environment where you just deploy the contract and it executes across many cores. Of course, you need to write the program in a way that will be executed on this multi-core machine, but before you write the program, you need to actually create this process. So what did TON do, and this is TON’s contribution to blockchain science, is that it created this virtual machine which allows for parallel execution; a multi-threaded asynchronous virtual machine, where every execution can be terminated with messages and sent to another virtual machine, which would then execute it's operations. And if we want to build this distributed parallel processor, we need to have an asynchronous core, like those on a physical processor, talking to each other and trying to execute operations really fast in parallel. And that's how this process should look. There is no such architecture in production today. The TON protocol concerns multiple BFTs that can achieve high throughput only theoretically. But as yet there has been no solution for functionality. Here are the requirements that we have set in front of us for Acki Nacki.

The basic mechanism of Acki Nacki; how it works in the most optimistic scenario where no one attacks the network:

* You need a block proposer, and then you need to apply that block as fast as possible to the state machines of other nodes. A block proposer is somebody who takes the transactions received from users, executes them inside the virtual machine, and sends it out to the network. This operation is quite fast. Now, if the block becomes too big and there are too many people who want to execute, then the block proposer splits the block into another block and another block and delegates the work to another block proposer. So now, instead of one big block, we'll have two smaller blocks, which will both be executed, in parallel, by two different block proposers. If you have a lot of load, theoretically, you'll have a network full of block proposers. Each of them will propose smaller chunks of this block.

* Now when they collate the block and they propose it to the network, it is sent to everyone in the network, and everyone happily applies, making the network pretty damn fast. How fast? Well, the whole network would operate off the time it takes to collate the block, according to the limited amount of transactions supplied to the block, and the broadcast time it takes to deliver this block to the validators and the other participants in the network. We unpack the block end-to-end and update the current local state with all transactions. So far, so good. This is the fastest theoretical way to update the state of the network. That's what Acki Nacki is. We could stop right here. The Acki Nacki block proposer takes the transactions, applies it to the block, and sends this block to everyone, every 330 milliseconds. And in roughly another 200 milliseconds on top of that, all other existing network participants will get the block, then unpack the block, and apply it to the state, which takes another 100, 120 milliseconds.

* All in all, Acki Nacki propagated these transaction results to the whole network in less than a second. We have a happy network of all nodes in sync…

*But what if someone is not honest?*



## **Ack/Nack/You’re ‘It’**
*What Acki Nacki Means.*

We need consensus, lest all involved propose whatever the hell they want. 

Enter Validators.


In Bitcoin the prerequisite to running the network is just to prove that you mined the hash. Once that’s satisfied you can happily produce the block, and everyone applies it. And if someone sees a mistake, they then simply accept another block by someone else. That's how it goes. And that's why it's slow.

In our case we say: “Wait a second. We need to validate this block somehow. So instead of proposing and waiting until another (correct) block will come out, let’s recognize that this is just one block proposal. It wasn’t everyone who created the block. If we don’t recognize this, then yes, it will take 13 minutes for all the blocks that could possibly pop up to be processed, and for the block to be accepted.” The solution we find, and one that is backed by the numbers, is as follows:


* What we're doing is amazingly simple. Let's imagine that we have a random number that is known to the network after the block was created by a proposer, that all agree upon, but that is not related to block validity — just a random number — and each validator will have their private key only known to them. Now let’s divide this random number by this private key and with [Modulo division](https://en.wikipedia.org/wiki/Modulo). If the Modulo ends with, for example, zero (0), then they know for themselves that they need to validate the book. A process entirely random and unpredictable

* Now we don't know how many Validators there will be, we don't know who they are, and the block proposer doesn't know who they are, meaning no collusion is possible. These random nodes will just validate this block. If they see that the block is not correct, they will send a negative acknowledgement/not acknowledged message (NACK) — [the definition](https://www.techtarget.com/searchnetworking/definition/NAK#:~:text=What%20is%20NACK%20): “a signal used by computers or other devices to indicate that data transmitted over a network was received with errors or was otherwise unreadable … sent by a recipient to report that a specific, expected signal must be re-sent for some reason … NACK messages often include the ability to report on the reason the message is being NACKed” — And if they see the block is correct, they will send an acknowledged message, or ACK. Hence why the protocol is called Acki Nacki

* The verifier isn’t just for posterity — it has teeth. **When a verifier finds that a block is not correct**, they will send the NACK message to the network and **the block proposer will be stripped of all of his money and be kicked out of the network immediately**.



## **Safety In Numbers**
*How Acki Nacki Is The Most Secure Consensus Algorithm*

Now let's prove the security guarantees this protocol actually provides.

This protocol offers greater protection, by several orders of magnitude, than Nakamoto consensus on the Bitcoin network. This is because the chances that a block proposer will issue an incorrect block and not be caught by verifier and be issued an ACK message is so slim, that it is significantly slimmer than an incorrect block being issued on Bitcoin. If a malicious block proposal has colluded with 49% of the network, the chances of them getting the next incorrect block without being NACKed is still (also) significantly lower than in Bitcoin. Moreover, even if a malicious actor has colluded with 49% of the validators and, in a [DDoS attack](https://www.fortinet.com/resources/cyberglossary/ddos-attack#:~:text=DDoS%20Attack%20means%20%22Distributed%20Denial,connected%20online%20services%20and%20sites), he pumped the other 51% of the network, — even with all that —the network will only stop, but will not be corrupted.

How? Well there are several possible attacks on this algorithm. One is an honest attack; I'm just a validator, I'm just a block proposer, who happens to have a malicious block. My chances of being accepted are significantly less than in Bitcoin. Then if one colludes with 49% of the network, again, the chances are slim. But what if an attacker gets creative? If someone sends a block to only a part of the network, let’s say to only 49% of the network, signed under the pretense of not having, not needing any consensus. Would that block be finalized if it won’t go to the whole network? Well, once every node on the network gets the block, without needing validation, this block will be signed, and a message will be sent with the hash of that block signifying the acknowledgement of its difference. In other words, everyone will know exactly what the case is, including that of possible maliciousness. The block is finalized not when the block is received, but only when the signatures of another X percentage of the validators of the network are obtained. Nothing is built from this block. You don’t explicitly check it. But the information about it is broadcasted to the majority of the network in an act that would exponentially mitigate future danger, seeing as any successive block will have an ever decreasing likelihood of receiving an ACK message. All this adds roughly another 200 to 300 milliseconds of delay to this block. And therefore we're saying it's about a second full second to the actual finality.

There is no attack that can corrupt the block with even minutely sufficient probability. Malicious block proposers will be NACKed in 99.999% of cases. We believe nobody will take that chance.

So what about trolls? Spammers who just produce one block after another in a giant wave? We bring up this question to illustrate another point about the interaction of finality and security in Acki Nacki. We need to wait for an ACK or NACK answer to be sent to the network. If we finalize the block too fast, a possible NACK will not reach all the validators. This is why, as we're going to release the block every 330 milliseconds, we're going to wait three blocks on average. A possible attack could be a block proposer introducing new blocks too fast, on the assumption that the blocks will already be finalized before a NACK is sent. Therefore, when the block proposer sends a block to the node, they must wait 330 milliseconds before an acknowledgement is sent out. This is not the case for the first block. But if the block proposer immediately follows that block with another block, the block will just wait. So even if the block proposer is starting to send many blocks at once, the network itself, through what we call the Broadcast Protection Mechanism, will also protect the timing at which blocks are verified to ensure a ACK or NACK message can always be sent; at, on average, 330 milliseconds per block, on top of the three stacked blocks. It’s worth noting that Acki Nacki is not a stacked protocol, but what it does is allow for sufficient time for the block to be finalized.

So what if a verifier will be lazy and won't verify any blocks? Well we have a mechanism protecting against that too. Upon detection, a lazy verifier will be slashed. So they have every incentive to be active.



## **What Did We Learn From All This?**
*Some Closing Thoughts*


We claim that the entire issue with Web3 is technological limitation. The decentralized world computer could not be built because blockchains today just can’t sustain it due to issues of gas prices, block size, throughput, and finality. That’s what led to effectively the only real application possible in Web3 being financial services. And any system dealing exclusively with financial services is always going to be a breeding ground for malicious actors, like scammers… Cue the exclamations: “Sam Bankman-Fried is blah blah!” We know. It’s a product of the design & its limitations.

But, one way or another, it won’t be that way forever. No doubt when simple word processors were hot stuff, OpenAI was pure science fiction. And right now blockchains are the word processors, and things like decentralized governments and a fully anonymous internet are the purview of Isaac Asimov imitators. What is not speculation is that technology will progress, and GOSH is at the forefront of this with Acki Nacki.

What the world computer will look like we do not know, but what we do know is that a multi-core-processor-like consensus is this next big step that will ensure it looks like something. Here we see a horizon of new worlds, that we will mold into the old one, but imbued with hope and possibilities for immense advancements.

My land in sight, a Kingdom of Peace… If only a man conquers her.

