### XCM_Overview.md
 
# XCM tl;dr
XCM is the format used to communicate between sovereign entities. It isn't a protocol, (from my understanding) XCM is to XCMP what HTML is to HTTP. XCM includes a lot of possible instructions, with receivers may only want to understand some subset. Unlike protocols native to different Blockchains XCM is abstract and well versioned, allowing it to be used for communication without knowing the specifics of the receiver. There are some examples of common uses of XCM: sending an asset within a Blockchain (from an address that you control on that Blockchain, to another address on that same Blockchain), teleporting an asset from one chain to another (burning it on the sending chain and minting it on the other), or putting an asset into reserve and creating a derivative on a different chain.


I am going to quote extracts from the article, and extrapolate a bit on what Dr Wood wrote.

*"To understand XCM better, it’s important to understand its boundaries and where it fits in the Polkadot technology stack. XCM is a messaging format. It is not a messaging protocol. It cannot be used to actually “send” any message between systems; its utility is only in expressing what should be done by the receiver."*

*"XCM aims to be a language communicating ideas between consensus systems. It should be general enough for it to be properly useful throughout a growing ecosystem. It should be extensible."*

### XCM is like a series of scripts that systems send to each other to modify each other's state.

*"In the parlance of XCM, we call this teleporting owing to the idea that the apparent movement of an asset in fact happens by destroying it on one side and creating a clone on the other side."*

### Possibly, you could use an XCM to instruct a SC on Ethereum to burn ERC-20 XXX tokens, which in turn follows up by sending another XCM message instructing a parachain runtime to mint SS58 XXX tokens(?). Edit: You thus minimise interaction with ETH gas fees payment mechanisms.

*"Finally, there may be two chains which want to nominate a third chain, one on which an asset might be considered native, to be used as a reserve for that asset. The derivative form of the asset on each of those chains would be fully backed, allowing the derivative asset to be exchanged for the underlying asset on the reserve chain backing it."*

### Possibly, you could use an XCM to instruct a BTC reserve chain's or bridge's runtime to mint specific BTC derivatives that can then be used on specific parachains (?).

*"At the core of the XCM format lies the XCVM. [...] In fact this stands for Cross-Consensus Virtual Machine. It’s an ultra-high level non-Turing-complete computer whose instructions are designed to be roughly at the same level as transactions.

The XCVM includes a number of registers, as well as access to the overall state of the consensus system which is hosting it. Instructions might change a register, they might change the state of the consensus system or both."*

### Possibly, you could use this high-level feature of XCVM to overcome the overreliance on cross-chain bridges (and their security risks!), choosing to work with cross-consensus instructions instead of cross-chain bridge transactions (?).

Given that BTC and ETH have crypto-treasures (i.e high value and most sought-after), you need the blockchain infrastructure to step up to meet their transaction security requirements. XCVM will have a very big role to play in this context.

---
# XCM Cross-Consensus Messaging
 XCM is the “cross-consensus” messaging format, rather than just “cross-chain”.  The XCM format is designed for communicating the kinds of ideas sent not just between chains, but also smart-contracts and pallets, and over bridges and sharded enclaves like Shared Protected Runtime Execution Enclaves (SPREE) sometimes referred to as "trust wormholes," [Polkadot’s Spree](https://wiki.polkadot.network/docs/learn-spree). 
 
- ### Not just cross-chain
- ### It's a format, not a protocol

# XCM Stack
[IMAGE HERE]


- Not just cross-chain
- It's a format, not a protocol

### Stack:
- **Pallets** uses `xcm-builder` crate
- **XCM** is the language for the format to talk to other chains
- **XCMP** is the actual transport protocol
- **VMP** (Virtual Message Passing) between relay and parachain
- **Bridges** use XCM for solochains
- **Custom Relays**, send to a pallet or smartcontracts


Goals for XCM
- Flexable
- Extensible
- General
- Suitable for on-chain
---
Why not native?
Destination-Specific

Why not us native APIs?
Obsoletable
Single transactions functionality limiting

Why not use Substrates dispatchables?
Fee payments doesn't fit

---
Initial use-cases
Optional fee payment
Remote & inter-chain transfer of funds
remote exchange
passing other assets
---

### Orders vs Instructions

Instructions are stand-alone
Orders operate on the Holding Register

XCM message is always an Instructions
Instructions often need to include Orders

---

## Teleport vs Reserved-backed Xfer

**Teleport** for transfers of dual-native assets between mutually trusting endpoints (*Faster, cheaper*)

**Reserved-backed** when endpoints must agree on third party holder until SPREE
(**slower, expensive**)


---

# Versioning of XCM

### v0
- Current XCM release v0.9.9
- API usable v0.9.10 + 6 months
- Forwards compatible XCM v1

### v1
- In development
- Scheduled for Polkadot v0.9.10
- Backward compatible XCM v0

---


# Versioning (v0.9.10 released)
### v0
- API usable v0.9.10 + 6 months
- Forwards compatible XCM v1

### v1
- API usable 6 months after v2
- Forwards compatible XCM v2

### v2
- In development
- Backwards compatable XCM v1

v0 continues in general use over the wire; upgraded v1-aware clients translate OTF


---
# Versioning
# v0.9.10 released + 4 weeks

### v0
- API usable v0.9.10 + 5 months
- Forwards compatible XCM v1

### v1
API usable 5 moths after v2
FOrwards compatible XCM v2

### v2
- In development
- Backwards compatible XCM v1

v1 in general use over the wire; chains < 0.9.10 no longer compatible
---

# Versioning 6 months later
- v0 is removed from the code base
- v1
- v2

---

# Versioning CoC
- Bump XCM, rebuild & deploy runtime < 4 weeks after new XCM release
- Update to latest XCM API < 6 months after release

---

# Caveat
- Compatibility not 100%
- Sooner the upgrade, the better

---

# Future

- Query response and success reporting
- Execution checkpoints
- Fail-safe "try-catch" handlers
- Safe transacting
- Governance over XCM standard moving forward

---

# Notes XCM

- Balance Transfers 
- shawntabrizi.com/xcm-workshop/#/

# XCM Executor
- Barrier

# XCM Config

- Simple Transfer
- Reserve Transfer
- Teleport Transfer

# Why is XCM so powerful?

Have you withdrawn USDT or USDC from an exchange before? If you have, then you'll probably notice that there's an option to chose networks like ERC-20, TRC-20, ALGO, MATIC, OMNI, etc... Those are blockchains, or ledgers, that says Person A transferred X token to Person B. Think of it as cars (or tokens) using different highways (or blockchains) to travel from Point A to Point B (one address to another). ERC-20 is the Ethereum blockchain, TRC-20 is Tron's blockchain, etc... and right now, if you send an ERC-20 token to a TRC-20 address, there is no guarantee that the funds sent are recoverable.

IF (and this is a huge IF) Ethereum, Tron, Algo, MATIC secures a parachain on Polkadot, it's not impossible for us to send tokens without caring about which blockchain we're using because any blockchain on Polkadot's network can communicate with each other using DOT as the base layer blockchain. It's also possible to do cross-chain swaps which are not limited by blockchains being siloed in their own highway. So imagine having a Polkadot DEX that can list way more tokens than Uniswap, Pancakeswap, Sushiswap combined WITHOUT needing to use bridges across blockchains.

I'm super hyped for this as it brings cryptocurrency one step closer to being idiot-proof and usable for the general population 
