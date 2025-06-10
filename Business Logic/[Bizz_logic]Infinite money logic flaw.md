# Lab: Flawed enforcement of business rules

**Category:** Business Logic  
**Difficulty:** Practitioner
**Lab Objective:**  
Buy the l33t jacket with coupon and insuff. funds. and gift cards.

---

## Application Flow

**Expected Workflow:**
login > signup to newsletter > get SIGNUP30 30% off coupon > buy and get 30% off

**Assumptions Made by Application:**
That the user will try to apply the same coupon twice in a row in the same cart.

**Hypothesis or Attack Surface:**
Buying 10$ gift cards at 30$ off and reusing would give me extra money.

---

## Observations

**Endpoints Involved:**
- Sign up for newsletter gives us a coupon code. We can buy gift cards.

**Behavior Noticed:**
- Coupon can be reused with different order.
- We can use gift cards bought by us

**Tools Used:**
- Proxy, Repeater, Intruder

---

## Exploitation Steps

1. Login, signup to newletter at bottom of the page.
2. add 13 gift cards to cart and get 30% off with coupon. 
3. send POST /gift-card to intruder and paste the gift card codes there.
4. Set max concurrent requests to 1 so money increases steadily.
5. Repeat till money > $1337
6. Buy jacket.

---

## Fix Recommendations

- Don't allow discout on gift cards
- Maintain coupon code history used by user?
