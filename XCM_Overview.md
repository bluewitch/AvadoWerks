### filename: XCM_Overview.md

# tl;dr
XCM is the format used to communicate between sovereign entities. It isn't a protocol, (from my understanding) XCM is to XCMP what HTML is to HTTP. XCM includes a lot of possible instructions, with receivers may only want to understand some subset. Unlike protocols native to different Blockchains XCM is abstract and well versioned, allowing it to be used for communication without knowing the specifics of the receiver. There are some examples of common uses of XCM: sending an asset within a Blockchain (from an address that you control on that Blockchain, to another address on that same Blockchain), teleporting an asset from one chain to another (burning it on the sending chain and minting it on the other), or putting an asset into reserve and creating a derivative on a different chain.

# XCM Cross-Consensus Messaging
- ### Not just cross-chain
- ### It's a format, not a protocol

# XCM Stack
IMAGE HERE


XCM Cross-Consensus Messaging

Gavin Wood @gavofyork


Not just cross-chain


It's a format, not a protocol

Stack:
Pallets uses xcm-builder crate



XCM is the language for the format to talk to other chains


XCMP is the transport protocol


VMP (Virtual Message Passing) between relay and parachain

Bridges use XCM for solochains

Custom Relays, send to a pallet or smartcontracts


Goals
Flexable
Extensible
General
Suitable for on-chain
---
WHy not native?
Why not us native APIs?
Why not use Substrates dispatchables?

Destination-Specific
Obsoletable
Single transactions functionality limiting
Fee payments doesn't fit

---
Initial use-cases
Optional fee payment
Remote & inter-chain transfer of funds
remote exchange
passing other assets


---

Orders vs Instructions

Instructions are stand-alone
Orders operate on the Holding Regigster

XCM message is always an Instructions
Instructions often need to include Orders

---

# Teleport vs Reserved-backed Xfer

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


