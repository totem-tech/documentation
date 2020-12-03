<h2>Comparison of Totem with the Traditional Accounting Process</h2> 

As mentioned elsewhere in these documentation pages, the tradtional flow of communicating accounting data is very broken. This page outlines the various steps in a traditional book-keeping process and compares with how Totem has condensed the entire flow into 2 simple steps.

### Traditional Accounting Process

> In tradional book-keeping for every sale that takes place in a business there are approximately 14 steps to carry out. That's a lot of work!

This is not an exhuastive list, but it is the minimum requirement to have the accounting records updated and correct in any accounting system. We have not included the granular data-entry tasks, but some important ones are also listed here.

Below this section you will see a comparison with the Totem process and how it removes many of these manual steps making the whole process orders of magnitude more efficient.

<h4> 1. Sales Invoice created by supplier</h4>

* Accounting
    * Supplier posts to accounts receivable 
    * Supplier posts to Sales Tax Control Account as a payable

<h4> 2. Invoice emailed to Client</h4>

This step is about communicating the invoice or receipt to the Client. Email is often used, but it could also be posted by mail or printed as a receipt at the time of purchase.

<h4> 3. Client receives Invoice</h4>

It is important to note that the Client considers this as a **Purchase Invoice** for accounting purposes.

* Accounting
    * Client posts to accounts payable
    * Client posts to Sales Tax Control Account as a receivable

<h4> 4. Client triggers payment from Client bank</h4>

<h4> 5. Supplier bank receives payment</h4>

<h4> 6. Bank statements issued (to both Client and Supplier from their respective banks)</h4>

This is a step that generally occurs once a month and is not universally automated. In some cases the book-keeper must request a copy from their Client, who may or may not provide the document in a timely manner. This step should _never_ be missed, late or overlooked, because it affects the business' cash-flow. 

The whole process includes then next two steps, and this also goes for step 12, 13, and 14.

<h4> 7. Statments uploaded to both sets of accounting software</h4>

<h4> 8. Statements reconciled with accounting records</h4>

* Accounting
    * Client reverses accounts payable
    * Client increase expenses
    * Client reduces bank balance in accounting
    * Supplier reverses accounts receivable
    * Supplier increase revenue
    * Supplier increases bank balance in accounting

<h4> 9. External declarations</h4>

This step is carried out once per quarter in Europe. Some businesses that handle cash payments choose to carry out this task once per month.

* Supplier submits Sales Tax declaration from control account
* Client submits Sales Tax declaration from control account

<h4> 10. Payment issued by Supplier to Tax Office Bank</h4>

A payment is necessary when the balance of Sales Tax declaration in the control account is in favour of the Tax Office. 

<h4> 11. Payment received by Client from Tax Office Bank</h4>

A payment is received when the balance of Sales Tax declaration in the control account is in favour of the Client (or in some cases the Supplier.)

<h4> 12. Bank statements issued (to both Client and Supplier from their respective banks)</h4>

<h4> 13. Statments uploaded to accounting software</h4>

<h4> 14. Statements reconciled with accounting records</h4>

* Accounting
    * Client reverses Sales Tax Control Account receivable
    * Client increases bank balance in accounting
    * Supplier reverses Sales Tax Control Account payable
    * Supplier decreases bank balance in accounting

---

### Totem Accounting Process

> There are in effect only 2 steps in Totem required to acheive the same book-keeping end result.

<h4> 1. Invoice created in Totem with one transaction</h4>

In Step 1 the blockchain automatically carries out book-keeping for both parties at once. The accounting receipes built-in to Totem handle the updates as follows (note this just one of many such recipes in Totem):

<h4> 1.a for Supplier Identity</h4>

* Blockchain posts to accounts receivable
* Blockchain posts to Sales Tax Control Account as a payable

<h4> 1.b for Client Identity</h4>

* Blockchain posts to accounts payable
* Blockchain posts to Sales Tax Control Account as a receivable

<h4> 1.c Different optics for Supplier and Client on same record</h4>

* Supplier sees the same blockchain transaction as a Sales invoice
* Client sees the same blockchain transaction as a Purchase Invoice

<h4> 2. Client triggers payment in Totem with one transaction</h4>

In Step 2, the blockchain carries out book-keeping for **all three concerned parties** at once.

The third-party in this case is the Tax Office administering Sales Taxes (VAT in Europe). Their records are also updated and payments between parties are effected immediately.

<h4> 2.a for Supplier Identity</h4>

* Blockchain reverses accounts receivable
* Blockchain increase revenue
* Blockchain increases bank balance in accounting
* Blockchain reverses Sales Tax Control Account payable

<h4> 2.b for Client Identity</h4>

* Blockchain reverses accounts payable
* Blockchain increase expense
* Blockchain decrease bank balance in accounting
* Blockchain increases Sales Tax Control Account receivable

<h4> 2.c for Tax Office Identity</h4>

* Blockchain increases Sales Tax Office (revenue) in accounting
* Blockchain increases Sales Tax Office bank balance in accounting
* Blockchain decreases Sales Tax Office (expense) in accounting
* Blockchain decreases Sales Tax Office bank balance in accounting

<h4> 2. External declarations</h4>

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
