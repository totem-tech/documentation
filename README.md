<h1>Introduction</h1>

<h3>Totem Live Accounting  is built on the idea that accounting ledgers should be able to communicate directly with each other, anywhere in the world, in real-time.</h3>

To achieve this we are in the process of developing a custom built blockchain runtime and a peer-to-peer network, coupled with a full set of account posting recipes to create - what we believe to be  - one of the first fully decentralised non-finance products for business and consumers anywhere.

> **You can think of Totem like a globally available, dedicated public network for accounting data with a modern, intuitive, usable front-end app.**

<h4>Technically speaking, Totem is delivering a fully functional accounting ledger attached to every blockchain wallet on its network.</h4>

Having said that, it is however, a *_gross under-representation_* of the greater project goals which are outlined elsewhere on the interwebs.

## Why is Totem important?

<h4>The communication flow in accounting and book-keeping is completely broken. Your email inbox is spammed full of accounting information like, invoices, Uber receipts, flight expenses, online orders, and there is no direct connection between those accounting documents, the payment, the reasons for the transaction, or crucially, <i>your</i> accounting system.</h4> 

Whichever way you try to manage this, it boils down to manual effort to  gather and send the information to your accountant, who re-encodes it _again_ and carries out much manual effort to reconcile these documents to business activities, payments, bank statements. 

Businesses large and small suffer equally with this same problem, ***because there is no common accounting protocol*** upon which to reconnect the pieces. This is the heart of the problem to be solved by Totem's work.

## What we are working towards...

<h4>In our view, when an invoice is created at, for example Uber, then it should <i>automatically</i> appear in your accounts. It should appear in the correct expense reporting, and it should already be flagged as settled, and the appropriate entries from your payment card, bank card should already have been made in your accounts as well.</h4>

Sounds obvious right? It hasn't been done before because there was no good peer-to-peer mechanism to build such a protocol for handling these types of accounting postings. **A blockchain solves this because by definition it is about communicating accurate verifyable information peer-to-peer.**

At Totem, we go one step further... this mechanism should not be dependent on a centrally controlled accounting software company, who will inevitably sell you licences and sell your data! This mechanism should be open to all, completely independent of  accounting software vendors, and continue to operate, peer-to-peer, at all times, forever. Even when Totem no longer needs to exist.

This is the problem that Totem has solved. Once you see this ability in action, _"much new thing possible"_.

## Story so far.

<h4>Totem is still an early stage product, as we started developing in earnest in December 2018 building on years of discovery and research, that evolved out of experimental projects in the blockchain and cryptocurrency space going back to 2013.</h4> 

The idea behind Totem is simple however and makes sense in a connected world. 

> Even if you are not running a business, the business of "accounting records" touches everything you do, like it or not. 

From the receipt for a new smartphone, to your regular groceries you are bombarded with accounting data you cannot easily make use of. 

Imagine a world where you could, for example, see how much you paid for tomatoes last year? Or five years ago? Or shoes, or speeding fines... without you having to do anything special. Imagine that the information just existsed privately, for you to access any time you wanted. How could that change your life? 

Honestly, we don't know, but it will be a bonus side effect of what Totem are building. 

Our main target market is the ever-expanding decentralised economy - as businesses employ less, and contract freelancers more, we are all moving towards a future where our accounting will be at the granular level of our identity. 

### The alternatives

<h4>Q: Can banks do what Totem is doing? A: No.</h4> 

The problem for banks is that their messaging system does not handle the details of each transaction, so the messages that banking systems receive are very basic. More importantly it is not _their business model_ to collect this data and so they do not. **We would argue that they are missing the opportunity.** 

<h4>Q: Can accounting software companies do this? A: Yes and no.</h4> 

The single biggest issue is that they all compete with each other - the coverage would not be universal. Additionally it would destroy their licence-fee paying business model, or in some cases the model that sells your data. What would happen to your data if the software company merged or stopped operating?

<h4>Q: Can any other business do this? A: probably.</h4>

Doing accounting software requires experience, but building accounting software that operates on a blockchain network, is an entirely different beast. It will require not only expertise in both domains, it will also require a vision about how peer-to-peer accounting entries can be made on a decentralised public network, what the risks are and how they can be mitigated. Given that most accountants still view blockchain as hot air, there is a lot of catch-up to do to catch the front runner - Totem. 

<h4>Q: Can Totem implement this? A: Yes..</h4>

The Totem team demonstrated this capability in February 2019, connecting five random parties and three tax jurisdictions, posting accounting entries in all relevant accounts on a blockchain. This was a "Marconi moment". Connecting ledger for the first time means the activity of accounting will change forever. 

We have been building out the full scale version ever since and Totem can already do many of the underlying communication tasks required to make this happen. We are actively pushing new code every day.

### Application Architecture

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

#### Privacy

The Totem Network will have privacy by default for all self-managed identities. The BOXKEYS is a key building-block in that process. 

As the development progresses we will be introducing fully encrypted storage and end-to-end communication (hence the reason for developing BOXKEYS and BONSAI) to maintain data security and privacy for everyone using self-managed identities on any Totem network. 

In the longer term we will be using Fully Homomorphic Encryption (FHE) for obvious reasons.

### Totem Meccano

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

We welcome anyone who wishes to contribute to this documentation and the code is open source. Please get in touch to contribute.