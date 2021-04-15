> **We are aware that there are a number of scam crypto projects claiming to be Totem. These scammers have no code repositories or have issued a smart contract scam tokens using our Totem brand. Please check the Polkadot community forums to ensure you are communicating with the genuine Totem Team.**

## Comparison of Totem with the Traditional Accounting Process

### This page outlines the various steps in a traditional book-keeping process and compares with how Totem has condensed the entire flow into 2 simple steps.

#### Traditional Accounting Process

> In tradional book-keeping for every sale that takes place in a business there are approximately 14 steps to carry out. That's a lot of work!

This is not an exhuastive list, but it is the minimum requirement to have the accounting records updated and correct in any accounting system. We have not included the granular data-entry tasks, but some important ones are also listed here.

Below this section you will see a comparison with the Totem process and how it removes many of these manual steps making the whole process orders of magnitude more efficient.

#### 1. Sales Invoice created by supplier

* Accounting
    * Supplier posts to accounts receivable 
    * Supplier posts to Sales Tax Control Account as a payable

#### 2. Invoice emailed to Client

This step is about communicating the invoice or receipt to the Client. Email is often used, but it could also be posted by mail or printed as a receipt at the time of purchase.

#### 3. Client receives Invoice

It is important to note that the Client considers this as a **Purchase Invoice** for accounting purposes.

* Accounting
    * Client posts to accounts payable
    * Client posts to Sales Tax Control Account as a receivable

#### 4. Client triggers payment from Client bank

#### 5. Supplier bank receives payment

#### 6. Bank statements issued (to both Client and Supplier from their respective banks)

This is a step that generally occurs once a month and is not universally automated. In some cases the book-keeper must request a copy from their Client, who may or may not provide the document in a timely manner. This step should _never_ be missed, late or overlooked, because it affects the business' cash-flow. 

The whole process includes then next two steps, and this also goes for step 12, 13, and 14.

#### 7. Statments uploaded to both sets of accounting software

#### 8. Statements reconciled with accounting records

* Accounting
    * Client reverses accounts payable
    * Client increase expenses
    * Client reduces bank balance in accounting
    * Supplier reverses accounts receivable
    * Supplier increase revenue
    * Supplier increases bank balance in accounting

#### 9. External declarations

This step is carried out once per quarter in Europe. Some businesses that handle cash payments choose to carry out this task once per month.

* Supplier submits Sales Tax declaration from control account
* Client submits Sales Tax declaration from control account

#### 10. Payment issued by Supplier to Tax Office Bank

A payment is necessary when the balance of Sales Tax declaration in the control account is in favour of the Tax Office. 

#### 11. Payment received by Client from Tax Office Bank

A payment is received when the balance of Sales Tax declaration in the control account is in favour of the Client (or in some cases the Supplier.)

#### 12. Bank statements issued (to both Client and Supplier from their respective banks)

#### 13. Statments uploaded to accounting software

#### 14. Statements reconciled with accounting records

* Accounting
    * Client reverses Sales Tax Control Account receivable
    * Client increases bank balance in accounting
    * Supplier reverses Sales Tax Control Account payable
    * Supplier decreases bank balance in accounting

---

### Totem Accounting Process

> There are in effect only 2 steps in Totem required to acheive the same book-keeping end result.

#### 1. Invoice created in Totem with one transaction

In Step 1 the blockchain automatically carries out book-keeping for both parties at once. The accounting receipes built-in to Totem handle the updates as follows (note this just one of many such recipes in Totem):

#### 1.a for Supplier Identity

* Blockchain posts to accounts receivable
* Blockchain posts to Sales Tax Control Account as a payable

#### 1.b for Client Identity

* Blockchain posts to accounts payable
* Blockchain posts to Sales Tax Control Account as a receivable

#### 1.c Different optics for Supplier and Client on same record

* Supplier sees the same blockchain transaction as a Sales invoice
* Client sees the same blockchain transaction as a Purchase Invoice

#### 2. Client triggers payment in Totem with one transaction

In Step 2, the blockchain carries out book-keeping for **all three concerned parties** at once.

The third-party in this case is the Tax Office administering Sales Taxes (VAT in Europe). Their records are also updated and payments between parties are effected immediately.

#### 2.a for Supplier Identity

* Blockchain reverses accounts receivable
* Blockchain increase revenue
* Blockchain increases bank balance in accounting
* Blockchain reverses Sales Tax Control Account payable

#### 2.b for Client Identity

* Blockchain reverses accounts payable
* Blockchain increase expense
* Blockchain decrease bank balance in accounting
* Blockchain increases Sales Tax Control Account receivable

#### 2.c for Tax Office Identity

* Blockchain increases Sales Tax Office (revenue) in accounting
* Blockchain increases Sales Tax Office bank balance in accounting
* Blockchain decreases Sales Tax Office (expense) in accounting
* Blockchain decreases Sales Tax Office bank balance in accounting

#### 2. External declarations

These are the Sales Tax returns, submitted monthly or quarterly.

* Supplier submits Sales Tax declaration from control account

* Client submits Sales Tax declaration from control account

---

### Steps made obsolete by Totem

These are the steps that are replaced or nullified from the original process?

5. Supplier bank receives payment
6. Bank statements issued (both Client and supplier)
7. Statments uploaded to accounting software
8. Statement reconciled
10. Payment issued by Supplier to Tax Office Bank
11. Payment received by Client from Tax Office Bank
12. Bank statements issued (to both Client and Supplier from their respective banks)
13. Statments uploaded to accounting software
14. Statement reconciled
