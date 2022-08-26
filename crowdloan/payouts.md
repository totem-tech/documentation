# KAPEX Crowdloan, Pledge & Referral Program Award Payouts

### This document details the awards payouts and calculations following the Totem Kapex Crowdloan, Pledge and Referral Programs which are all now closed.

Totem won Auction #20 on Polkadot and secured a parachain slot for the KAPEX Parachain and in return we will be paying out KAPEX to the community that helped us reach this milestone.

_This process does not yet include a payout for the migration of users from the Totem Meccano Canary Network as these will follow the distribution and go-live of the Production KAPEX Parachain._

You can find the published allocations and payouts in a [Public Google Spreadhseet](https://docs.google.com/spreadsheets/d/13asCuALay7faQl7HZBhaiQDEZVGA-LUIHz-STlsjSYw/edit?usp=sharing) which contains the following sub-sheets:

* Summary Accounts

* KAPEX Payouts

* DATA: Combined Crowdloan Pledge & Referral

* DATA: Referrals

* DATA: Referred by ID

_It should be noted that google sheets does not handle 12 decimal places correctly sometimes. This may result in the last 4 decimal places being replaced by zeros. Your actually allocations however will be correct to the last decimal place._

## tl;dr

**_You will be delighted to hear that you are all going to receive many more KAPEX than you expected due to the effects of the low turnout and the guaranteed minimum distribution._**

Although the Google Document and this documention page explains the exact calculations for the entire payouts including referral rewards, you can calculate the minimum amount that you will receive using the formulas below:

> Use the Multipliers below with your Crowdloan and Pledge DOT contributions to validate your Crowdloan and Pledge Award _including your allocation of the 22% guaranteed distribution_ as stated in our documents and now the published distribution document._*_

_*If the published amount in the KAPEX Payout sheet are more than expected, it is because the following calculation does not include Referral Rewards, which are calculated seperately._

**Constants**

| Description | Amount | Currency |
|---|---|---|
|Total DOT Contributed in the Crowdloan	|132833.41217905|DOT  |
|Total DOT Contributed in the Pledge	|9059.7899999993|DOT  |
|Guaranteed Minimum Distribution Amount	|568000         |KAPEX|
|Allocation Factor	                    |3.2            |     |	

**Crowdloan**

|Crowdloan Payout Multiplier _calculated as follows_|
|:-:|
|Guaranteed Minimum Distribution Amount|
| divided by|
|(Total DOT Contributed in Crowdloan + (Total DOT Contributed in Pledge * Allocation Factor))|
|**3.5099701033**|

**Pledge**

|Pledge Payout Multiplier _calculated as follows_|
|:-:|
|Guaranteed Minimum Distribution Amount|
| divided by|
|(Total DOT Contributed in Crowdloan + (Total DOT Contributed in Pledge * Allocation Factor)) * Allocation Factor|
|**11.2319043305**|

### Referral Program

Our original proposal for the Referral Program was that we would pay the Referer 5% of the Referee’s **DOT contribution**, and that the Referee would also receive this same bonus.

However considering the low turnout in the Crowdloan and Pledge offerings the total payout shared amongst all who took part in the referral program would have been a **puny 555.364879999997 KAPEX!**

We therefore decided to update the Referral Payout to be based on the Referee’s KAPEX award _after_ the uplift not the actual DOT contribution of the referee. 

> This change has meant that all users who took part in the Referral Program will now receive a minimum 3410% greater than expected referral reward!

More information about how we calculated this is in the detailed breakdown below.

## Detailed KAPEX Payout Breakdown

**_This section is for anyone that wants to look into the details of the distribution or audit our calculations. We recommend that contributors who are interested do so [informing us](mailto:support@totemaccounting.com) if they discover any issues._**

## Summary Accounts Sheet

In the first sheet in the Google Document we have published a high-level view of the allocations. All values in this sheet are rounded to the nearest KAPEX unit.

We start with the facts concerning the Crowdloan, Pledge and Referral Program.

|Description | Amount | Currency |
|---|---|---|
|Total DOT Contributed in the Crowdloan	    |132833	|DOT|
|Total DOT Contributed in the Pledge	    |9060	|DOT|
|Total KAPEX to be Allocated from Crowdloan and Pledge	|570899	|KAPEX|
|Total KAPEX to be allocated from Referral Program	|24169	|KAPEX|

* The "**Crowdloan, Pledge & Referral Allocations**" and "**Current Team Allocations**" are the initial payouts derived from details in other sheets. 

* There will be no vesting on these amounts and users are free to transfer as soon as they are received.

* The "**Treasury**" of the Live Accounting Association (_in formation_) retains the remaining balance following distribution of circa 1,728,568 KAPEX.

* This amount will be allocated according to our documentation and as described ion the "**Treasury Balance Breakdown**" section on this sheet.

## KAPEX Payouts Sheet

The second sheet provides the calculation mentioned above as well as a table containing funds distributed from the Crowdloan, Pledge and Referral Offerings by address.

> Tip: You can search for your address to find the amount of KAPEX you will receive including all referral bonuses.

## DATA: Sheets

The last three sheets contain data that has been used to create the calculations and provide a level of detail for auditing.

**DATA: Combined Crowdloan Pledge & Referral Sheet**

This sheet is designed as a simple list with some indicators and allows slicing and dicing the data using Pivot tables.

**DATA: Referrals Sheet**

This contains the data that allowed us to calculate the percentage of referral reward payout for each address. Note the following:

* Not all addresses are listed here - only those that are in the referral programs.

* Addresses that either did not have a referer ID or referer address are excluded. The qualification for this was that both the referer and the referee must have taken part in the Crowdloan, and if one of them did not then this would disqualify both from receiving a referal rewards.

* Addresses that are seen as both Referee and Referer contributed via ParallelFi. ParallelFi decided to assign their referral rewards to their users meaning that ParallelFi users will receive both the referral reward for having been referred by ParallelFi as well as the Referee reward from ParallelFi. ParallelFi also supplied with a list of addresses and the amounts contributed, so that we were able to make this analysis.

    * We have not officially received any confirmation regarding other Centralised Exchanges (CEXs) that aggregated contributions to the Crowdloan nor which addresses are officially theirs. On that basis we have no means to included the referral rewards from contributions made via CEXs. We suggest that if this is the case for you that you contact the CEX that you contributed through and ask them to contact us to resolve.

**DATA: Referred by ID Sheet**

This sheet is designed so that referers can identify the amounts contributed by the accounts they had referred. We have not shown the referer addresses for privacy reasons.