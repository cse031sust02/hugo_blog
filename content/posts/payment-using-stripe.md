---
date: "2017-04-10T15:27:28+06:00"
title: "Accepting payments on your site using Stripe"
---

---

## What is [Stripe](https://stripe.com/)?
A popular payment processor. It accepts payments from customers around the world on web or in mobile apps.
  
### Payment types
Stripe accepts all major debit and credit cards in 100+ currencies. It also supports bank and direct debit payments, local payment wallets, Alipay and cryptocurrency (Bitcoin) etc.

---

## Accepting Payments with Cards

Using card information with Stripe is a two-step process

1. Securely collect payment information using tokenization
2. Use the payment information in a charge request or save it for later

### Step 1 : Securely collect payment information using tokenization
Stripe provides three methods for tokenizing customer’s payment information over HTTPS
Checkout, Stripe.js & Mobile SDKs

#### 1. [Checkout](https://stripe.com/checkout)
The easiest way to integrate Stripe is via Checkout, an embedded tool that takes care of building an HTML form, validating user input, and securing your customers' card data. Using Checkout, sensitive credit card information is sent directly to Stripe, and does not touch your server. customers can pay instantly, without being redirected away to complete the transaction.

In addition to credit and debit cards, Checkout supports Alipay and Bitcoin too. more types of payment coming soon.

Checkout has 12 languages to pay with a localized experience.

Embedding checkout in your site
https://stripe.com/docs/checkout/tutorial

#### 2. [Elements](https://stripe.com/docs/quickstart#elements)
If we want to customize the payment form for our need, then we can make use of Stripe Elements.

#### 3. [Mobile SDKs](https://stripe.com/docs/mobile)
Stripe has native libraries for iOS and Android applications.

### Step 2 : Use the tokenized payment information
While a token is created on the first step, now the token is used by our server-side to make an API request to Stripe. Two common examples of when you would use a token are :

#### Charging the customer immediately
We can create a one-time charge request to charge a customer’s card. 

The API request will contain the token, currency, amount to charge, and any additional information we may want to pass. [more details..](https://stripe.com/docs/quickstart#charge-immediately)

#### Saving the customer’s card information
If we’d like to have the ability to charge the customers again in future (without them needing to enter their payment information again), we can create an API request to store their payment details inside a customer record instead. [more details..](https://stripe.com/docs/quickstart#saving-card-information)