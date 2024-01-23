# TERP_CAT
a repository of information on OP_CAT compiled by Terp and Team

The Bitcoin Improvement Protocol (BIP) OP_CHECKTEMPLATEVERIFY (CTV) is a proposal that aims to enhance Bitcoin's scripting capabilities. It introduces a new opcode, OP_CHECKTEMPLATEVERIFY, which is designed to enable more complex smart contracts while maintaining security. The primary focus is on improving the efficiency and flexibility of Bitcoin's scripting language.

RGB (Rust, Bitcoin, and Lightning) is a layer 2 protocol built on top of Bitcoin. It facilitates the creation and management of tokens (colored coins) on the Bitcoin blockchain. RGB aims to provide a scalable and privacy-focused solution for tokenization, allowing users to issue, transfer, and trade tokens securely without relying on a separate blockchain.

Stacks is a layer 2 protocol associated with the Stacks blockchain, which is designed to bring smart contracts and decentralized applications (DApps) to Bitcoin. Stacks utilizes a unique consensus mechanism called Proof of Transfer (PoX) and connects to the Bitcoin blockchain for security. It enables developers to build smart contracts and DApps on top of Bitcoin while benefiting from Bitcoin's security model.

In summary, OP_CHECKTEMPLATEVERIFY focuses on improving Bitcoin's scripting capabilities, RGB layer 2 focuses on tokenization on the Bitcoin blockchain, and STACKS layer 2 enables smart contracts and DApps on a separate blockchain (Stacks) connected to Bitcoin. Each addresses different aspects of functionality and use cases within the broader Bitcoin ecosystem.

The proposed opcode, OP_CHECKTEMPLATEVERIFY (CTV), is designed to have a significant impact on Bitcoin by introducing a commitment hash parameter that requires transactions executing the opcode to include outputs matching the commitment. This introduces the concept of a covenant, allowing the creation of addresses with specified spending conditions.

Initially named OP_CHECKOUTPUTSHASHVERIFY (COSHV), the proposal focused on congestion control transactions, where a spender pays a single address using CTV. Once confirmed to a suitable depth, this assures multiple receivers that they can each be paid. The two-step process resembles payment batching but has the potential to further reduce fees.

Subsequent versions of the proposal expanded its scope, highlighting the ability to create various contracts and covenants using the new opcode. This includes the creation of channel factories, vaults, and coinjoin transactions in novel ways, potentially simplifying construction and reducing fees. Additionally, there is speculation about using the opcode to allow users to trustlessly pool their funds into a single UTXO, enhancing privacy.

However, criticisms of the proposal have surfaced, with concerns that it may be too specific to the congestion control use case and lacks a generic covenant capability. Despite the criticisms, the introduction of OP_CHECKTEMPLATEVERIFY holds promise for enabling diverse and innovative applications within the Bitcoin ecosystem beyond its initial focus on congestion control.

New LNHANCE combination soft fork proposed: Brandon Black posted to Delving Bitcoin details about a soft fork that combines previous proposals for OP_CHECKTEMPLATEVERIFY (CTV) and OP_CHECKSIGFROMSTACK (CSFS) with a new proposal for an OP_INTERNALKEY that places the taproot internal key on the stack. Authors of scripts must know the internal key before they can pay to an output, so they could directly include an internal key in a script. However, OP_INTERNALKEY is a simplified version of an old suggestion from CTV’s original author, Jeremy Rubin, to save several vbytes and potentially make scripts more reusable by allowing the value of the key to be retrieved from the script interpreter.

In the thread, Black and others describe some of the protocols that would be enabled by this combination of consensus changes: LN-Symmetry (eltoo), Ark-style joinpools, reduced-signature DLCs, and vaults without presigned transactions, among other described benefits of the underlying proposals, such as CTV-style congestion control and CSFS-style signature delegation.

As of this writing, technical discussion was limited to the request about what protocols the combination proposal would enable.

OP_CAT PROTOCOLS:

What does Bitcoin future looklike with OP_CAT enabled? Bitcoin with speed Bitcoin with privacy Bitcoin with increased size and scalability

Bitcoin App structure v Bitcoin Data Structure How RGB focus heavily on bitcoin data structure

Real world applications

Privacy and Flexibility Improvements: The Taproot upgrade is designed to bring improvements to Bitcoin's privacy and flexibility. Taproot introduces a new scripting language called Tapscript, and the integration of Schnorr signatures, which can enhance the privacy of transactions by making them look more uniform on the blockchain. Avoiding Network Splits: The focus on different activation strategies, such as BIP 9, BIP 8, and Modern Soft Fork Activation, is aimed at preventing network splits during the upgrade process. This is crucial to maintaining the integrity and coherence of the Bitcoin network. Upgrade Coordination: The article discusses various methods for coordinating upgrades among Bitcoin nodes and miners. The goal is to ensure a smooth transition from the old rules to the new rules without causing disruptions or creating factions within the network. Potential Impact on Miners: The debate over activation methods, including discussions on forced signaling and miner incentives, reflects a consideration of how miners might be affected by the protocol changes. The goal is to find a balance that encourages miners to upgrade while avoiding unnecessary delays or risks. OP_CAT (OP_CHECKTEMPLATEVERIFY): Bitcoin Improvement Proposals (BIPs) often introduce new opcode operations, and OP_CAT builds on the Taproot upgrade.

the proposal to reintroduce an old opcode in Bitcoin called OP_CAT, which was part of Bitcoin's original scripting system and enabled the concatenation of two strings. The opcode was disabled by Satoshi Nakamoto in 2010 due to concerns about potential vulnerabilities. Taproot Wizards, a group promoting Ordinals, believes it's time to reinstate OP_CAT to enhance Bitcoin's functionality without requiring a hard fork.

Udi Wertheimer of Taproot Wizards suggests that while OP_CAT doesn't create a full-blown smart contracting language like Ethereum, it enables functionalities such as decentralized exchanges and bridging assets. Unlike Ethereum, Bitcoin intentionally had limited programmability for simplicity and security. Re-enabling OP_CAT is considered a relatively simple change, involving around 10 lines of code in Bitcoin Core.

One advantage of OP_CAT is that it would only require a soft fork, making it less contentious than a hard fork. This aligns with the trend of recent proposals, like BitVM, aiming to expand Bitcoin's utility without necessitating a hard fork. OP_CAT's reintroduction is seen as beneficial for projects like BitVM, and some Bitcoin forks, like Bitcoin Cash, have already re-enabled OP_CAT.

Taproot Wizards has also introduced "evolving inscriptions," demonstrated by the Quantum Cats project, a limited edition set of 3,333 cat images with pre-programmed characteristics revealed over time. The article emphasizes the technical and political challenges faced by Bitcoin developers, aiming to bring more attention to their work and promote a similar energy of improvement as seen in Ethereum.

Udi Wertheimer suggests that Bitcoin, while being slow to change, should undergo deliberate upgrades to better serve billions of people. This discussion concludes by acknowledging the ongoing discussions and challenges within the Bitcoin governance process.

John Law proposes using covenants, specifically OP_CHECKTEMPLATEVERIFY and SIGHASH_ANYPREVOUT, to address scalability issues in large channel factories for the Lightning Network (LN). The challenge arises when signature-based protocols involving a large number of users, such as coinjoins or previous factory designs, encounter disruptions, rendering collected signatures useless. Covenants are suggested as a solution, allowing a small transaction to restrict its funds to predefined child transactions, which can also be limited by a covenant.

Law's model involves creating a timeout tree, where a funding transaction pays into a tree of predefined child transactions, subsequently spent off-chain into numerous separate payment channels. This design enables efficient creation of millions of channels with a single small on-chain transaction. After expiration, the factory funder can reclaim funds with another small on-chain transaction, and users can withdraw their funds over LN to other channels prior to expiration.

Law also introduces modifications to the Fully Factory Optimized Watchtower Free (FFO-WF) protocol, offering advantages for the covenant-based factory design. Notable benefits include the ability for the factory funder to move funds for casual users from one factory to another without user interaction, enhancing trustless control and reducing the likelihood of on-chain transactions close to expiry.

Concerns are raised about the "thundering herd" problem, where the failure of a large dedicated user could lead to many users putting time-sensitive transactions on-chain simultaneously. Law mentions working on a solution, inspired by Gregory Maxwell's idea to delay expiry when "blocks are full," addressing this issue and aiming to publish the design when finalized.

Links: https://www.rgbfaq.com/faq/what-is-rgb https://bitcoinops.org/en/topics/op_checktemplateverify/ https://blockworks.co/news/op-cat-bitcoin-taproot-wizards https://www.quantumcats.xyz/bip-land https://taproot.watch/ https://jimmysong.medium.com/bitcoin-uasf-and-skin-in-the-game-7695031c5689 https://bitcoinmagazine.com/technical/bip-8-bip-9-or-modern-soft-fork-activation-how-bitcoin-could-upgrade-next https://github.com/terpdoctor/DED77_CAT/tree/main
