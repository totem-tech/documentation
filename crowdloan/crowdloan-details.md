# Calculations for Totem KAPEX Allocations

In this section we outline the details of the allocation mechanisms for Totem’s KAPEX Parachain Crowdloan and Pledge.

### Base Calculation

> Minimum Crowdloan Participation :  **5 DOT** <br />
> For every **1 DOT contributed** you will receive a minimum of **0.1 KAPEX**.<br />
> _This does not include bonuses (see below)_

**The total quantity of KAPEX minted is 2,581,818 KAPEX coins.** 

* **55% of all coins - 1,420,000 KAPEX** are available to supporters of the Crowdloan and Pledge.

* If we reach our **Soft Cap contribution of 1M DOT** we will award all participants a **10%** increase in awards.

* If we reach our **Target Cap ontribution of 10M DOT** we will award all participants a further **10%** increase in awards, making a **total 20% bonus**.

### The Referral Bonus 

Each participant in the Crowdloan can also benefit from referring a friend, and when that friend contributes in the Crowdloan, you will both receive a split bonus of 5% of the contributed funds in the crowdloan. 

* this only applies to the amounts committed into the Crowdloan - you will not receive a bonus on any amounts pledged by your friend.

### The Pledge

**Reminder: The Pledge is a non-binding signal of intent to help fund the development team, actionable only if a parachain slot is won. DO NOT SEND FUNDS when you Pledge.**

Totem is a small highly motivated development team. We have been founder funded since we began building our network in 2018, and now we are ready to grow our team, and accelerate the development to market.

You can chose to **pledge up to a maximum 10% of the quantity of DOT committed in the Crowdloan**. In exchange your receive a bonus calculated below.

> Bonus Bonus: The Pledge amount is **also included in the calculation for Soft and Target Cap bonuses!**

#### Pledge Award Calculation

By signalling an amount of DOT in the Pledge, you will be able to claim a multiplier of Totem KAPEX calculated as follows:

> **Ratio of commitments**:
>
> Total quantity of DOTs signalled in the pledge / Total quantity of DOTs committed in Parachain Crowdloan

> **Total DOT Commitment**:
>
> Total quantity of DOTs signalled in the pledge + Total quantity of DOTs committed in Parachain Crowdloan

> **Multiplier**
>
> Total DOT Commitment * (1 + Ratio of commitments) * 0.1

### Soft and Target Cap Success Bonus

Regardless of whether you participated in the pledge or not, the total DOT contributed (plus any bonuses) is the basis for the *Cap Success Bonus.

### Airdrop

Totem’s Meccano userbase will have their balances migrated to the KAPEX network allocating the 77,455 KAPEX prorata basis. 


## Other information

**Commitment Limits**
* For the Crowdloan there are no upper limits for participants, but a minimum of 5 DOT is required to participate.
* A minimum commitment of 0 DOT is applied for the Pledge.
* The Ratio of commitment is capped at 10% per address. 
  * There is no benefit to over-pledging but you will be required to submit the correct amount to make the bonus claim.

_There are implied limits to participation proportional to the Crowdloan limits and the Pledge limits set out above._

**Lock Periods**
* The DOT contributed towards the Crowdloan are locked for the period of the parachain lease and can be reclaimed thereafter.
* KAPEX is awarded if the parachain Slot auction is won, and will be carried out on chain.
* A balance transfer lock will apply to all KAPEX awards for a period of time following a parachain win. This will give the team time to generate the funds and apply it to the participating Polkadot addresses. 
* Once the allocations of KAPEX have been completed, transfers will be enabled. 

## Example

In the following table, Column A has committed & pledged the highest amount but the lowest ratio of commitments, Column B has not taken part in the Crowdfund, and Column C has the lowest amount committed, with the highest ratio of commitment.

This should give you a good idea as to how KAPEX is awarded.

| Description                         | A      | B      | C    |
|-------------------------------------|-------:|-------:|------:|
| DOT Committed in Crowdloan          | 100    | 80     | 1     |
| Basis KAPEX Coins awarded           | 50     | 40     | 0.5   |
| Pledged DOT                         | 2      | 0      | 0.1   |
| Ratio Pledged to Crowdloan          | 2%     | 0%     | 10%   |
| Total DOTS                          | 102    | 80     | 1.1   |
| Soft Cap Reached 10% Bonus in KAPEX  | 5.000  | 4.000  | 0.050 |
| Target Cap Reached 20% Bonus in KAPEX  | 10.000 | 8.000  | 0.100 |
| Total KAPEX awarded @ Soft Cap      | 57.020 | 46.436 | 0.700 |
| Total KAPEX awarded @ Target Cap      | 62.020 | 50.436 | 0.705 |

*_These are examples, there are no limits to the amounts you can commit, and the values are calculated at the time of writing. They calculations may be subject to change up to 48 hours before the auction starts._

## Links

This section contaiuns the links on how to participate in the auctions and other useful information.

[Parachain Candle Auction Research](https://research.web3.foundation/en/latest/polkadot/economics/3-parachain-experiment.html)






### KAPEX Coin Supply

|                                                      | Supply % | KAPEX       |
|------------------------------------------------------|---------:|------------:|
| **Total Supply KAPEX**                               | **100%**     |  **2,400,000**  |
| KAPEX Released Crowdloan & Pledge                    | 55%      |  1,320,000  |
| Current & Future Team                                | 20%      |  480,000    |
| Polkadot Community & Airdrop                         | 5%       |  120,000    |
| Live Accounting Association <br />Dev & Engineering Grants | 20%      |  480,000    |

The video shows you the steps you will need. It is based on Polkadot’s evil twin network Kusama, but the steps are identical. Credit goes to Jay Chrawnna for publishing it - check out his [channel](https://www.youtube.com/playlist?list=PLtyd7v_I7PGkrOymjT8HwD-_x9VP8Tads) - it’s awesome and very funny too.
<iframe width="800" height="315" src="https://www.youtube.com/embed/K_16N6CeJyo" title="Participate in Corwdloans" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>