+++ 
draft = false
date = 2020-12-22T14:37:10Z
title = "Handling financials in your app - best practices"
description = "Handling money in your app is tricky and can lead to upset customers and loss of revenue. Here are some examples how you can improve DX and reduce future bugs."
slug = "financials-best-practices" 
tags = ['javascript', 'financials']
categories = []
externalLink = ""
series = []
+++

This blog is not about how to integrate Stripe or arrange payments. This is mostly about how to name your variables. As you know, naming variables is the second most difficult problem in software engineering.

Money is a highly sensitive topic, and if you are tasked with the implementation of money related features, there are a few things to consider. This primer will apply to JavaScript-based apps, and we are going to look at both frontend and backend parts of the solution. Some practices could be extrapolated and used in general to improve code maintainability - like verbose variable namings. But this is mainly a collection of learned practices from several production projects I've been involved in the past couple of years, serving millions of customers.

## ToC

- [Units and currencies](#units-and-currencies)
- [Variable naming](#variable-naming)
- [Calculations](#calculations)
- [Frontend](#frontend)
  * [Convert pence to pounds and pence](#convert-pence-to-pounds-and-pence)
  * [Apply locale-based currency formatting](#apply-locale-based-currency-formatting)
  * [User inputs](#user-inputs)
- [Bonus round: Roundings](#bonus-round--roundings)
- [Summary](#summary)

## Units and currencies

So, let's talk money.

Since I'm based in London, Britain used to have the most amazing currency system. Up until the year 1971, we used to have pennies, shillings and pounds. 12 pence would make a shilling, and 20 shillings would amount to a whole pound. Luckily today most countries in the world have adopted decimal-based currencies, where there are generally 2 different units of money - like pounds and pence. A pound today equals to a 100 pence, and that's it. No halfpence, shillings or other base-12 units. (fun fact - if you prefer base 12 numbers and currencies, you are a _dozenial_)

This makes things significantly easier for us today. But a few challenges remain.

1. There are still 2 units of money to handle - pounds and pence
2. JavaScript is horrible with floating point math

If you've been dealing with Stripe API or other similar money processing services, you'll notice that among other things they've chosen to represent all monetary values as integers in a currency’s smallest unit. This approach is called [Zero-decimal currencies](https://stripe.com/docs/currencies#zero-decimal). For us this will mean that **all values are in full pence** - and consequently are integers. This elegant choice solves both of the above-mentioned problems in a single sweep, since:

1. There's only one unit of money to handle now
2. JavaScript is mostly ok with integer-based math

As far as backend goes, we can handle and store all values as integers aka pence / cents / insert your smallest unit here. If you are starting a new project, this could be a convention you introduce on a team level. However, if you are in the middle of the ongoing project, a few challenges arise. Likely, money is already handled and stored in some way. It is also likely that it was stored as floats, with pounds and pence. This is how we as humans handle monetary values since elementary school.

It is also likely that variables and database columns containing money would likely be called "amount" or "refundAmount" or something along the lines. There is a common understanding about the representation of the monetary "amount", and it is likely not what you want it to be.

Here we are going to introduce a key convention. **All variable names must contain units if there is a unit involved**. This way there is no ambiguity about the representation of the value.

One of the catastrophic software bugs in space was in 1998 when Mars Climate Orbiter [crashed into the planet](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter) instead of successfully slowing down itself into Martian orbit. The reason was two separate software modules relying on each other but using 2 different units to represent impulse produced by thrusters. Software integration is indeed where things often fall apart.

## Variable naming

Name of a variable should reflect its content - I hope this is something we can all agree on. When you walk through the code, a variable name should be verbose enough to tell you its purpose.

Imagine now if we have a function that accepts money amount inputs and produces a money amount output:

```javascript
function calculateRefund(shippingCost, paidAmount) {
  return shippingCost + paidAmount;
}
```

Would this pass a code review? It probably would, especially if we supply a few unit tests. A nice pure function, well tested indeed.

Now, `shippingCost` is supplied by a separate service, which has everything in pence. This way we end up in a situation when two arguments are supplied, one in pence amount, another in pounds and pence. There will be no errors, however, the outcome of our function would suddenly be very much off.

Let's refactor things a tiny bit.

```javascript
function calculateRefundInPence(shippingCostInPence, paidAmountInPence) {
  return shippingCostInPence + paidAmountInPence;
}
```

Everything is more verbose now, but also it is much clearer what this function expects as inputs, and what kind of output will be returned - function name contains a promise of a unit now.

In TypeScript you could make things clearer with strict typings:

```javascript
function calculateRefund(shippingCost:number, paidAmount:number):number {
  return shippingCost + paidAmount;
}
```

But even then you'd still have to provide a custom type with an implicit name like `Pence`:

```typescript
type Pence = number;

function calculateRefund(shippingCost:Pence, paidAmount:Pence):Pence {
  return shippingCost + paidAmount;
}
```

This brings a good level of clarity, but even then I'd argue that having `InPence` as part of the variable and function names is simpler, more effective and much more human-readable.

Of course, this is not limited just to functions and variables. The same convention applies to component properties, DB column names and anything else that contains or deals with monetary values.

## Calculations

JavaScript is notoriously bad with floating comma math. Try this in your browser's console:

```
1.23 + 0.61
=> 1.8399999999999999
```

Turning everything into integers helps to a certain point, but even then you might struggle with things like division and rounding to the nearest pence. There are libraries like [Decimal.js](https://mikemcl.github.io/decimal.js/) that give better control over the decimal related math.

In any case, you probably want to contain business logic and perform it most safely. Ideally on a backend. Send inputs, calculate and render output on the client. If you are in control of the full picture, you could have all the amounts always converted to pence, and only at the very last moment presented as pounds and pence for user's convenience.

![](https://alexsavin.me/photos/2020-12-22-poundsInPenceChart.png)

## Frontend

I'll use React terminology, but the same goes for any component-based framework. The main challenge of the client-side is this is where you want to represent monetary value in the most familiar format for the user. This means turning `45783` into something like `£ 457.83`.

It is worth pointing out that some currency symbols are widely available in popular fonts, while others might not be. Also, some currency symbols are displayed in front of the value, while others are displayed after. Oh yes, and some countries prefer commas, while others like points.

Is this all? Well, some countries also like to separate large amounts with spaces, like `£ 1 000 000.00`. And of course, even if the value is in full pounds, you still want to display zero pence aka `.00`. But not in Kenya - oh no. Some countries are ok with full amounts and no pence, please.

How international is your app after all?

There are generally two stages of presenting a currency value received from the backend.

### Convert pence to pounds and pence

Could be as simple as `amountInPence / 100`.

Of course, you can never be sure with floating comma math and JavaScript. To be safe you probably want to validate the result of the calculation. Or use a library like `Decimal.js`. Or both. 

### Apply locale-based currency formatting

A rare case when standard JS library is perfect for the job. Meet [Intl.NumberFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat):

```javascript
const currencyFormatter2 = new Intl.NumberFormat('en-gb', {
  style: 'currency',
  currency: 'GBP',
  minimumFractionDigits: 2,
  maximumFractionDigits: 2,
});

currencyFormatter.format(234.8)
=> "£234.80"
```

### User inputs

There will be a need to allow users input of pounds and pence. There are a few ways of approaching this, but the general idea would be to allow decimals input and then convert it into pence value before sending it to the backend. Ideally, as soon as possible.

There are a few ways of approaching this, but one way is to contain pounds and pence input in a dedicated component. For this purpose you can make a custom input component that uses `onChange` event, immediately converts the value into pence and passes this forward to the rest of the app where everything is always represented in integer pence.

Of course, implicit variable and prop naming is especially important in places where we have the same amount represented in different units. `amountInPence` and `amountInPounds` is the convention we have adopted for such scenarios.

## Bonus round: Roundings

If you are dealing with complex business logic involving division, you might have to address a topic of accurate rounding. In a scenario where multiple calculations occur before the final result is returned to the user, it may be off by a few cents because of multiple roundings occurring as part of every step of the calculation.

For example:

```javascript
function roundToFullPence(amountInPence) {
  // performs rounding to the nearest full pence
}

const refundAmountInPence = 38733;
const partialRefundInPence = 
  roundToFullPence(refundAmountInPence / 100 * 33.33);
=> 12910

const TAX_RATE = 22.5;
const refundWithTaxInPence = 
  roundToFullPence(
    partialRefundInPence + (partialRefundInPence / 100 * TAX_RATE)
  );
=> 15815 // final result

```

However if you as a user decide to double-check this calculation, you will end up with `15814.3934025`, which is, even when rounded, 1 penny less then what we've come up with.

There are a few ways of addressing this, assuming you are sticking with JS environment and there are no other alternatives at this time of the day.

* Increase precision of the lowest denomination. Traditionally we said that everything should be stored as integers representing full pence amounts. Banks, however, prefer storing everything with extra level or two of precision. So, still integers, but instead of full pence, we go after one-tenth or hundredth of a pence.
* Only apply rounding at the very last moment. This is something that requires full control over the business logic pipeline, and it will require removing any extra rounding steps that might occur along the way towards the user (or the DB).
* If you are not in a position of control over the full pipeline, you can implement integrity checks at the very end of the calculations. Integrity check is effectively a more streamlined re-implementation of the amount calculation, where you calculate a second value and compare it to the output of the "official" pipeline. This way you control the roundings, and if there are discrepancies in the comparison, you can opt to apply a correction to the final value before outputting it to a user.

## Summary

Handling money in your app is tricky and can lead to upset customers and loss of revenue. But if nothing else, these two things can make your life easier:

* Have units as part of variable / prop / function names, like `inPence` or `inPounds`
* Convert amounts to the lowest denomination and have it as whole integers everywhere in the app
