<h1>About Totem</h1>

<h2>Totem | Live Accounting is part of the Polkadot Ecosystem.</h2>

<h3>Totem Live Accounting  is built on the idea that accounting ledgers should be able to communicate directly with each other, anywhere in the world, in real-time.</h3>

To achieve this we are in the process of developing a custom built blockchain runtime and a peer-to-peer network, coupled with a full set of account posting recipes to create - what we believe to be  - one of the first fully decentralised non-finance products for business and consumers anywhere. 

> **You can think of Totem like a globally available, dedicated public network for accounting data with a modern, intuitive, usable front-end app.**


<h4>Technically speaking, Totem is delivering a fully functional accounting ledger attached to every blockchain wallet on its network.</h4>

Having said that, it is however, a *_gross under-representation_* of the greater project goals which are outlined elsewhere on the interwebs.

<h3> Why is Totem important?</h3>

<h4>The communication flow in accounting and book-keeping is completely broken.</h4> 

> Your email inbox is spammed full of accounting information like invoices, Uber receipts, flight expenses, online orders, and there is no direct connection between those accounting documents, the payment, the reasons for the transaction, or crucially, <i>your</i> accounting system.

Whichever way you try to manage this, it boils down to manual effort to  gather and send the information to your accountant, who re-encodes it _again_ and carries out much manual effort to reconcile these documents to business activities, payments, bank statements. 

Businesses large and small equally suffer with the same problems ***because there is no common accounting protocol*** upon which to reconnect the pieces. 

**This is the heart of the problem that Totem aims to solve**.

<h3> What we are working towards...</h3>

<h4>In our view, when an invoice is created at for example Uber, it should <i>automatically</i> appear in your accounts. It should appear in the correct expense account and it should already be flagged as settled, with the appropriate entries from your payment card.</h4>

Sounds obvious right? It hasn't been done before because there was no good peer-to-peer mechanism to build such a protocol for handling these types of accounting postings. A blockchain solves this because by definition it is about communicating accurate verifyable information peer-to-peer.

At Totem, we go one step further: this mechanism ***should not be dependent on a centrally controlled accounting software company***, who will inevitably sell you licences and worse, _sell your data_. 

This mechanism should be open to all, completely independent of  accounting software vendors, and continue to operate, peer-to-peer, at all times, forever.

These are the problems that Totem is solving. Once you see Totem in action, [sic] _"much new thing possible"_.

<!-- <h3> Application Architecture</h3>

There are several key features of the Totem Architecture which are as follows:

* the blockchain runtimes, accounting recipes, and on-chain storage, 
* full homomorphic encryption (FHE) for debit and credit entries, ensuring nobody (not even the blockchain itself) can see your  accounting figures.
* the Totem BOXKEYS on-chain public key registry, 
* the Totem BONSAI on-chain pre-authentication for off-chain distributed NoSQL databases,
* the off-chain distributed NoSQL storage (using the Totem BONSAI protocol of course), 
* the off-chain global shared datasets (companies, products, places), 
* encrypted storage on- and off-chain,
* the front-end UI service, 
* the p2p encrypted communication channels, 
* socially recoverable identities,
* the 'transactions' faucet,

Most of the components are designed to allow businesses to participate in the global live accounting network, but they can also run their own private networks should they wish to do this, and still benefit from being able to communicate with other companies and exchange account posting information.

Whilst much of this is established in an early form, we are on course to complete development sometime in 2021, you can view the progress on our live network https://totem.live[Totem Live Accounting]

#<h3> Privacy</h3>

The Totem Network will have privacy by default for all self-managed identities. The BOXKEYS is a key building-block in that process. 

As the development progresses we will be introducing fully encrypted storage and end-to-end communication (hence the reason for developing BOXKEYS and BONSAI) to maintain data security and privacy for everyone using self-managed identities on any Totem network. 

In the longer term we will be using Fully Homomorphic Encryption (FHE) for obvious reasons.

<h3> Totem Meccano</h3>

The current version of the Totem network is the  *Meccano TestNet*. We do not plan a MainNet until we have a fully functional end-to-end product. This will likely be in later this year (2020 as of writing).

The purpose of this network is to begin wider engagement with the blockchain community, monitor performance and interactions in all parts of the architecture, adapt the economic model, and obviously upgrade, fix and battle-test the code. Please send us an mailto:info@totemaccounting.com?subject=Inquiry:%20I%20want%20to%20participate%20in%20Totem%20development[email] if you want to be part of the team.

You can already test and use much of the core communication and storage technology as well as the first modules which have already been built, including: 

* Identities,
* Partners,
* Activities,
* Teams,
* Timekeeping,
* Transfers, 
* BOXKEY Server,

There is also a bleeding edge (read "sometimes broken") live development network https://dev.totem.live[here]. If you are a developer, you can see our entire group of developments at various build stages https://gitlab.com/totem-tech[here].

When using Totem Meccano via the links we recommend you experiment with friends, partners and other businesses (this is a peer-to-peer service after all) to get the general idea about how we are connecting and posting between parties. 

If you come across any issues, or wish to make suggestions for develoment or user experience please take the time to post them https://gitlab.com/totem-tech/issues/new[here].


## Welcome to Totem Live Accounting Docs.

**In these pages you will find supporting documentation on the Totem Live Accounting application and other detailed aspects of the project.**

Here we expand upon concepts in the various modules of Totem, and explain the vision as we see it and how that relates to what we are building.

> Totem Live Accounting is a global peer-to-peer real-time accounting ledger designed for the gig economy. 

What that means is that accounting entries are posted directly into all independent parties’ accounts as soon as they are created by a transaction or a business event. The ability to conduct accounting updates with anyone, anywhere at anytime, closely matches changes to employment in the economy at large. More workers are being employed in the gig-economy and are becoming increasing reliant on peer-to-peer interactions.

With traditional accounting software peer-to-peer communication is impossible. In some cases competitors have tried to provide a similar solution but this always relies upon all parties subscribing to the same software. This rarely happens, and there are many risks and issues associated with doing this especially as the solutions are centralised and worse, you do not control your data. 

Totem innovates this because the protocol which we are building allows companies to share data without configuration securely, privately and without having to rely on a software vendor. Alongside the protocol, we are also building a user interface (aka UI) so that companies can use the Totem protocol immediately without having to build an interface themselves - although they could if you wanted to.

## The Concept of Totem Modules

In broad terms "a module" in Totem is an item that can be found in the navigation bar of the UI. It usually has two primary components: the front-end user interface (Totem UI) and the back-end blockchain (Totem Network).

## Supporting Services for each Totem Module

There are additional supporting components which allow your data to be stored locally on your device, and this in turn is supported by a remote service which syncronises your data with your device and the blockchain. 

In the UI itself there is a queuing mechanism that helps with sending transactions and synconisation.

All these services will be explained here too. 

## Contribution

We welcome anyone who wishes to contribute to this documentation and the code is open source. Please get in touch to contribute. -->