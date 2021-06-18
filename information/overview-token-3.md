> **We are aware that there are a number of scam crypto projects claiming to be Totem. These scammers have no code repositories or have issued a smart contract scam tokens using our Totem brand. Please check the Polkadot community forums to ensure you are communicating with the genuine Totem Team.**

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

The calculation is as described in the following table. It should be noted that USD was used as the currency to measure the Total Market Cap. This results in a price of TOTEM in USD. However any currency could have been used as a measure and the end result would be a price in that other currency. 

| Steps to calculate TOTEM exchange rate                                                                         | Values              |
|--------------------------------------------------------------------------------------------------------------|--------------------:|
| Sum the "Total Market Cap" (TMC) of all assets in USD                                                        | 126441464918052     |
| Sum the Total Units (irrespective of currency) - "Total Market Units" (TMU)                                  | 37441006590481700   |
| Divide the TMC by the TMU to get the Notional Unit Price (NUP) in USD per market unit                        | 0.003377085         |
| Index Reference Value (IRV) Homage to Euler's Number                                                         | 2718281828459045235 |
| Define the ratio of TMU to IRV (TMU/IRV = IRVr)                                                              | 0.013773777         |
| Multiply NUP by IRVr. **This is TOTEM Price in USD**                                                           | 0.0000465152        |

_The values for TMC and TMU are current at the time of writing._

> The exchange rate of TOTEM fluctuates in balance with the fluctations in the Reference Exchange Rates and so represents a stable Unit of Account against which all currencies can be measured. This makes it an ideal candidate as a Functional Currency.

In Totem all accounting enries are recorded in TOTEM by default. The entres are made at the exchange rate of the moment of recognition and not the value in the currency that the transaction is made. In this way all accounting entries are recorded directly in the Functional Currency. As per our example above and do not require further adjustments. The adjustment occurs automatically when producing the statements in the Presentation Currency.


### Totem Global Currencies Index.

In addition to this calculation it is possible to derive a "Global Currency Index" value for KPI's on the world economy: 

| Calculate "Starting Global Currency Index"                                                  | Index  Starting Value |
|---------------------------------------------------------------------------------------------| ---------------------:|
| Invert IRVr                                                                                 | 72.60                 |

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

Simply put, owning TOTEM means that you are a stakeholder in all the Totem Test Networks and the future MainNet. The success of the network does not depend on you, but your holding has value when you use Totem or release that value now or in the future in the planned OTC marketplace.

**The Token Issuance is discussed in the next section.**