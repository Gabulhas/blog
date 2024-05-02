---
title: "The (unproved) argument that the Trillema is Undeniable"
date: 2023-05-24T00:37:33+01:00
draft: false
---

!!DRAFT!!


Notice: Whatever I said in this post I hope that someday it has been proven false. Even though that sometimes we think stuff is impossible, most of the time they turn out to be possible ;)


I've been reading a lot on Twitter about how network X or network Y have solved the "Blockchain Trillema", but usually they don't refer to all the facts and most of the time this is said by X or Y bagholders.

I'm not a fanatic of any specific network, I'm interested and unbiased (IMHO) when it comes to this type of thing.

I can say that I'm biased when talking about aesthetic design choices in these projects. 
Nothing beats a pretty-looking site, colors, logo, and the whole ecosystem's aesthetics (look at [Fantom](https://fantom.foundation/) ghost/spooky aesthetic, or [Solana's](https://solana.com/) colors and minimalism), but this is beside the point.

For those that don't know what is the Blockchain Trillema, check this post: [Why sharding is great: demystifying the technical properties](https://vitalik.ca/general/2021/04/07/sharding.html)

## Summary of the Trilemma 
Basically, there are 3 main proprieties that define a blockchain (or blockdag, or any of these types of networks), and these are: 

**"Scalability"** (sometimes also called speed, or throughput), can be thought of as how many transactions a network can handle at a given time (not only).
This is influenced by the following factors (and more):

**"Decentralization"**, can be thought of as the amount of power over the network is distributed. If only one of the participants (of the network) has control over a network, the network is the most centralized. If every participant of the network has the same power over the network itself, the network is the most decentralized. When I mean participant I don't mean only the number of nodes of the network. If 1 or more nodes are managed by a single entity (like a CEX), then those nodes count as only one participant. 

**"Security"** You can think of the threshold of how many attackers or attacks a network can withhold. It refers to the ability of the network to resist attacks and fraud. 


**It's said that you can't achieve the most of each one in a single network. There are always trade-offs!**

# Trillema in layman's terms

So another way to reason about this is the following: 
If I want to increase Decentralization, I will have to give up on some Security or Scalability, or a bit of both, and vice-versa.

In "layman's terms", you can think of these three things as the following example: 

Imagine you're organizing a meeting for a large group of people (let's say 1000 people) in a hall. You want everyone to participate equally (decentralization), you want to ensure no one interrupts the meeting or causes chaos (security), and you also want to make sure that the meeting can accommodate even more people if needed (scalability) and the meeting to happen as fast as possible, so people don't waste time.

**Decentralization**: Everyone in the meeting has an equal say in the discussion. There's no single leader who has the final say, and decisions are made collectively. This is similar to a decentralized blockchain where all nodes in the network participate in the validation of transactions.

**Security**: You need to ensure the meeting is secure and that no one can disrupt it. This might include having some rules in place to maintain order. Similarly, in a blockchain, security is about ensuring that the transactions and the network as a whole are secure from malicious actors.

**Scalability**: If more people want to join the meeting, you need to make sure the hall can accommodate them. In the blockchain world, scalability refers to the ability of the network to handle a growing amount of work and its potential to be enlarged to accommodate that growth. The meeting should happen as fast as possible. You can relate this to block time, finality, and TPS in the blockchain.

So you can now think of ways that increasing one of the parameters, one or both of the other parameters would have to decrease, so here are some examples:

- The more people there are:
    - the more time it the meeting should take, because people chatter making it harder to spread the message, more people have different opinions(making decisions harder to make), etc
    - bigger is the chance that someone will disrupt the meeting or something wrong happens

- The faster the meeting should go and the bigger the hall
    - There should be more security, to prevent chaos and disruption

If you want to have a more structured meeting with clear guidelines and rules (increased security), it may take longer to make decisions (decreased decentralization) as discussions might be more controlled and limited.

If you want to accommodate a larger number of people in the meeting (increased scalability), it might be challenging to ensure equal participation from everyone (decreased decentralization) as larger groups can be more difficult to manage.

If you aim for faster decision-making and efficiency in the meeting (increased scalability), it might be necessary to have a designated leader or authority figure (decreased decentralization) who can make quick judgments and keep the discussion moving.

If you want to maximize decentralization and ensure everyone's voice is heard (increased decentralization), it might be harder to enforce strict security measures (decreased security) as it can be challenging to control and monitor the actions of all participants, also, the meeting would have to take longer if anyone would speak.

If you prioritize high levels of security to prevent disruptions (increased security), it may limit the number of participants (decreased scalability) as stricter security measures can make it more difficult for new people to join the meeting.


## Real Examples

Let's take at some real examples:
- Bitcoin: The network is pretty decentralized (let's ignore the pool's problem for now), where this network has the biggest number of participants, and it's pretty secure, as there are long block time creations, a lot of work being used to operate the network, yet, it's super slow. At most, Bitcoin has a TPS (transactions per second) of 7, and it usually takes 60 minutes for a transaction to be accepted as "final".
- Solana: The network **looks** pretty decentralized (with around 1800 validators as of May 2023), and it's pretty fast (usually at 3k TPS, but can reach 710k). But the network is also really secure. So what's the catch? I will explain it later. But Solana didn't solve the trilemma! And neither any of the blockchains you hear about online.

So can we pinpoint in a deterministic/"mathematics" way how secure, decentralized, and scalable a network is?

We can for both Security and Scalability, but not for decentralization, because decentralization isn't just a matter of the power that each participant has.

# How can we measure these aspects of the network?

For Security, there are well-defined and proven thresholds when designing a protocol (for example, if a participant has over 51% of the power in Bitcoin, it can control the evolution of the network) and other well-defined behaviors.

For Scalability, you can measure it using multiple ways, like, Transactions Per Second, Finality Time, and others.

But Decentralization not only is related to the underlying protocol but the network topology, structure, philosophy, and more.
Here are some of the factors that influence decentralization:
- **Number of nodes in the network**: The quantity of nodes plays a significant role in determining decentralization.

- **Requirements to run a node**: Often overlooked, this factor affects decentralization. Networks that allow running nodes on low-spec devices enable broader participation, fostering decentralization. Contrasting the requirements to run a [Solana Node](https://docs.solana.com/running-validator/validator-reqs) versus a [Bitcoin Node](https://bitcoin.org/en/full-node#minimum-requirements), the former demands industrial-grade hardware while the latter can be operated on a Raspberry Pi or an older computer.

- **Actual hardware running a node**: The hardware used to run a node influences decentralization. Networks relying on specific cloud providers like AWS introduce centralization risks, as the provider can choose not to offer their services to certain software users.

- **Topology of the network**: If a network separates validation nodes from history/storage nodes, centralization can occur around nodes with the most information. While using a phone for validation might seem decentralized, the ledger still needs to exist somewhere for validation and historical purposes, typically handled by specific nodes.

- **Distribution of power**: Mining Bitcoin using individual computers does not guarantee decentralization. Often, individuals combine their mining power into pools to increase their chances of receiving rewards. These mining pools can exert control over certain aspects of the network, such as transaction inclusion in blocks and transaction ordering.

- **Geographical distribution**: The geographic distribution of nodes can impact decentralization. If a majority of nodes are concentrated in a specific region or controlled by a particular organization, it can introduce centralization risks. A more dispersed distribution of nodes across different regions or countries can enhance decentralization.

- **Governance and decision-making**: The governance structure and decision-making processes within a network can influence decentralization. If decision-making power is concentrated in the hands of a few entities or individuals, it can lead to centralization. On the other hand, networks that involve a wider community in the decision-making process and employ decentralized governance mechanisms promote greater decentralization.

- **Incentives and rewards**: The incentive mechanisms and rewards offered by a network can impact decentralization. If the incentives heavily favor a small group or disproportionately benefit specific participants, it can lead to centralization as participants strive to maximize their rewards. Networks that design incentives to encourage broad participation and distribute rewards more equitably tend to foster decentralization.

- **Interoperability and compatibility**: The ability of different protocols or networks to interoperate and be compatible with each other can impact decentralization. When protocols are interoperable, it allows for a more decentralized ecosystem where different networks can communicate and interact seamlessly. In contrast, if networks are siloed or have limited compatibility, it can lead to centralization as participants are restricted to a single network or ecosystem. Take for example Layer 2 solutions. This somewhat increases the network decentralization but Layer 2's are usually more centralized themselves.

- **Centralized Figures**: If there are figures/influencers that have control over the network, then the network is way more centralized. Take for example Vitalk Buterin. Even though that Ethereum is decentralized, Vitalik has a lot of influence over the network's future. Same applies to Anatoly Yakovenko or Andre Cronje.



# Conclusion

In conclusion, the Blockchain Trilemma presents a fundamental challenge in designing decentralized systems. It states that achieving high levels of decentralization, security, and scalability simultaneously is a complex task. While improvements have been made in addressing the trilemma, no single network has definitively solved it.

Decentralization, security, and scalability are interconnected factors that require careful trade-offs. Networks that prioritize one aspect may face compromises in the others. The number of nodes, hardware requirements, network topology, power distribution, geographical distribution, governance, incentives, and compatibility all play a role in determining the level of decentralization.

However, decentralization itself is a nuanced concept that extends beyond the technical aspects of a protocol. It encompasses network topology, philosophical principles, community engagement, and more. Quantifying decentralization in a deterministic or mathematical manner remains challenging due to its multifaceted nature.

When people mention that the network they are bag-holding solved the trilemma problem, they usually overlook one or more aspects of decentralization.
Want to know what is fast and secure? Typical Bank transfers and Centralized Databases. So when you only focus on these two aspects you are trying to sell a mostly centralized cryptocurrency.

Despite the complexities, the pursuit of decentralized systems is crucial for fostering transparency, inclusivity, and resilience. However, it is essential to recognize that achieving complete decentralization may not always be feasible or desirable in every scenario. Striking a balance between decentralization, security, and scalability requires thoughtful considerations and ongoing refinement.

As the blockchain ecosystem evolves, continued research, innovation, and community participation will contribute to advancements in addressing the trilemma and pushing the boundaries of decentralized technology.

It is important to approach discussions and claims about solving the trilemma with a critical mindset, considering the various factors at play and the inherent challenges involved in achieving a truly decentralized system. Continued exploration and dialogue will help drive the progress needed to navigate the trilemma effectively and build robust, sustainable decentralized networks.
