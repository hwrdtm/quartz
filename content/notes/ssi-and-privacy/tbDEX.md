---
title: tbDEX
---
TBDEX is the first system that the TBD team has produced.

tbDEX is a decentralized, permissionless liquidity discovery protocol that unlocks financial services by enabling individuals to directly on-ramp and off-ramp between traditional and decentralized financial systems, creating a marketplace for compliant currency exchanges where wallet applications and liquidity providers can seamlessly interact.

The protocol has no opinion on anonymity as a feature or consequence of transactions. Instead, it allows willing counterparties to negotiate and establish the minimum information acceptable for an exchange.

It acts as a bridge between the permissionless world of digital currencies and the traditional world of fiat money. As a liquidity protocol, it enables these two distinct financial systems to communicate. Additionally, tbDEX facilitates fiat-to-fiat exchanges since it's designed to operate fluently with both digital and fiat currencies.

# How Does It Work

## Actors

- **[Wallet Apps:](https://developer.tbd.website/docs/tbdex/wallet/overview)** These hold identifiers and credentials, acting as an agent to facilitate exchanges on behalf of a person seeking liquidity
- **[PFIs:](https://developer.tbd.website/docs/tbdex/pfi/overview)** The entities offering liquidity services on a tbDEX network
- **[VC Issuers:](https://developer.tbd.website/docs/tbdex/issuer/overview)** Organizations that act as sources of verifiable credentials

## Messages

- **Request for Quote (RFQ)**: a request for the PFI to provide a quote specifically for the user based on the financial exchange they are requesting, the payment methods provided, etc. The RFQ also includes the proof of required credentials.
- **Quote**: a formal offer from a PFI detailing exactly what the user will receive in exchange for a specific currency or asset, as per their RFQ. It also includes the total fees associated with the chosen payment methods, instructions for making the payment and receiving the funds, and an expiration time after which the terms of the quote are no longer guaranteed.
- **Order**: an agreement to execute the transaction. At this time, both parties have agreed upon a settlement method for the transaction and can smoothly off-ramp from the tbDEX platform to the desired method of settlement.
- **Order Status**: updates on execution of the order, sent by the PFI.
- **Close**: signifies that the exchange has reached a terminal state. It can be used if the PFI is unable to provide a guaranteed quote to the RFQ, if Alice is no longer interested in the quote, if the order has failed, or if the order has completed. No messages can be added to an Exchange after a Close has been sent.

## Example Scenario[​](https://developer.tbd.website/docs/tbdex/#example-scenario "Direct link to Example Scenario")

Alice holds a digital wallet that securely manages her identity, including her identifiers, credentials, and authorizations for external apps and entities. Alice wants to exchange 100 units of digital currency for USD. Because Alice is off-ramping from digital currency to fiat, most PFIs are required to verify Alice’s identity in order to fulfill their regulatory and compliance obligations.

1. **Alice** informs her wallet of her need to make the exchange.
2. **Alice's Wallet** discovers PFIs that offer this currency pairing, compares their credential requirements with the VCs Alice holds, and if necessary, applies for any missing VCs.
3. The **Credential Issuer** (if applicable) issues the required VCs to Alice, which are stored in her wallet.
4. **Alice’s Wallet** presents the offerings to Alice, allowing her to choose the one she’d like to transact with.
5. **Alice** considers the reputation of the PFIs as well as the transaction fees before choosing a PFI.
6. **Alice's Wallet** creates a request for a quote (RFQ) with Alice's DID, the details of her request, and the required VC - which Alice has already obtained from another PFI in the past.
7. The **PFI** receives the RFQ, verifies the credentials, and responds with a quote.
8. **Alice's Wallet** accepts the quote by placing the order.
9. The **PFI** sends order statuses to the Wallet to update Alice about the order.
10. The **PFI** fulfills the order then sends a close message to Alice’s Wallet.

# Questions

**How does the PFI (Participating Financial Institution) send information to Alice's Wallet? Is Alice's Wallet actually a server that can receive incoming requests?**
- When a PFI onboards, they will be required to specify a `serviceEndpoint` in their DID.
- This `serviceEndpoint` routes to a server that is maintained by the PFI such that it understands how to handle user requests, eg. RFQs.
- Therefore, "sending information" is actually more like Alice's agent (Wallet application, eg. embedded agent in browsers) "retrieves information" from the PFI's running servers.

**How does a PFI make themselves known to Wallet applications?**
- When PFIs create a DID for themselves, they also register a `serviceEndpoint`. When using the web5 SDK to create a DID, PFIs can choose to publish the DID Document using the DID DHT method to Web5's DHT.
- I suppose PFIs can share their DID through any of their existing distribution channels (official website, socials etc.) and apps can resolve that DID using the Web5 resolver.

**How are DWNs used in this protocol?**
- TBD

# Resources
https://developer.tbd.website/docs/tbdex/