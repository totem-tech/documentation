

# How is TOTEM valued as a Unit of Account?

> **TOTEM has an exchange rate that is derived from a very large basket of assets.**

At the time of writing this basket consists of:

* 150 Fiat currencies 

* 90 Cryptocurrencies

* 503 Corporate currencies 

The motivation for including so many assets is that is that large variations in [Reference Exchange Rate](/information/overview-token-3?id=sources-of-data) values for any one of these currencies, does not skew the overall value of the basket. It is designed to be this way in order to deal with the high volatility of cryptocurrencies.

> The deterministic value will have miniscule variations on a daily basis and therefore is very stable.

**Note:** _The original specification for this value calculation from the original 2016 white-paper has changed to address the massive skewing affect that the price of Bitcoin BTC has had on the crypto markets. We do not anticipate that the calculation will change in future as simulations have indicated that the TOTEM exchange rate is now very stable._

### Steps to calculate TOTEM exchange rate.

The calculation for the Unit of Account is based on the **Nominal Effective Exchange Rate (NEER)** which has been enhanced to consider the weighting according to the total issuance of each coin in the basket. For fiat currencies this is a difficult to track as figures are somewhat unreliable, however with cryptocurrencies the equivalent of M0 Money Supply is very reliable. 

The weight **$w$** of the currency is calcualted as **$$w_i = {s_i^{-1}}\cdot{(\sum_{j=1}^n {s_j^{-1}})^{-1}}$$** which is the inverse issuance of each currency, multiplied by the sum of all inverse issuances for all the individual currencies in the basket. This provides a weighting by currency where the lowest issued currency (which is technically more scarce) is weighted greater than a currency that is heavily issued.

The weight adjusted price **$p_{wa}$** for each currency can therfore be calculated using the weight **$w_i$** and the price in base currency **$p_i$**: 

**$$p_{wa} = \sum_{i=1}^n w_i \cdot p_i$$**

The base currency can be any currency as long as it is consistent for the basket at the point of calculation. In other words the prices have to be expressed in the same currency when applying new data. 

For example if you are defining the Unit of Account for GBP, and the exchange rate you have is GBP/USD then USD exchange rate must be applied to the entire basket so that the Unit of Account is consistently applied. This does not mean that the value of the Units of Account are pegged to the US Dollar, because this calculation would hold even if another currency such as the Euro (and hence the Euro exchange rate) was used to determine the Unit of Account.

The Unit of Account **$u_a$** for each currency is derived by summing the weight adjusted prices **$p_{wa}$** to create a financial index **$f_{idx}$** 


**$${f_{idx}} =  {\sum_{k=1}^n p_{wa_k}}$$**

Apportioning a Unit of Account value to each currency by dividing the weight adjusted price by the financial index.

**$$u_a = p_{wa} \cdot {({f_{idx}})^{-1}}$$**



> The exchange rate of TOTEM fluctuates but maintains an accurate ratio between all exchange rates and so represents a stable Unit of Account against which all currencies can be measured. This makes it an ideal candidate as a Functional Currency for an accounting system.

In Totem all accounting entries are recorded in TOTEM by default. The entries are made at the exchange rate of the moment of recognition and not the value in the currency that the transaction is made. In this way all accounting entries are recorded directly in the Functional Currency. As per our example above and do not require further adjustments. The adjustment occurs automatically when producing the statements in the Presentation Currency.

### Totem Global Currencies Index.

In addition to this calculation it is possible to derive a "Global Currency Index" value **$G$** for KPI's on the world economy. This is simply the inverse of **${f_{idx}}$** value:

**$$G = {({f_{idx}})^{-1}}$$**



### Sources of data.

The data is sourced from so-called Central Bank Reference Rates. These are exchange rates that are published by all Central Banks and forms the basis of an official rate used for accounting purposes.

In the case of cryptocurrencies which do not have a Central Banks, the rates are provided in conjunction with [Chainlink](https://data.chain.link)‘s price feed oracles.

In the case of the Corporate Currencies the values are currently based on the Stock Exchange prices, but will later migrate to be fully managed on-chain currencies in the Live Accounting Network. 

### What about payments?

The beauty of cryptocurrencies is that they can be used to make payments. In addition to all the functionality described above, TOTEM is mainly used to pay for using the accounting functions, but the last part of the process is the use of TOTEM to settle invoices. 

Although Totem will handle recording accounting entries when payments are made using the existing financial system (of course) at some point those accounts need to be reconciled with your accounts.

> It is our view that businesses will inevitably realise that invoices can be settled with TOTEM because it has a stable and system-wide accepted value in preference to other currencies, including cryptocurrencies. 

**_This is our end goal._**

## So what does owning TOTEM mean for me?

Simply put, owning TOTEM means that you are a stakeholder in all the Totem Test Networks and the Polkadot Parachain and eventually the MainNet. The success of the network does not depend on you, but your holding has value when you use Totem or when you release that value now or in the future using the planned OTC marketplace.

**The Token Issuance is discussed in the next section.**