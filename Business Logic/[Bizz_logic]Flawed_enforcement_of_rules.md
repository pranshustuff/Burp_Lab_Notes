# Lab: <Lab Title>

**Category:** Business Logic  
**Difficulty:** Apprentice
**Lab Objective:**  
Buy the l33t jacket with coupon and insuff. funds.

---

## Application Flow

**Expected Workflow:**
login > add item to cart > apply 5$ off coupon > buy item

**Assumptions Made by Application:**
That the user will try to apply the same coupon twice in a row

**Hypothesis or Attack Surface:**
Maybe I can apply the coupon multiple times and get the price to near zero.

---

## Observations

**Endpoints Involved:**
- Sign up for newsletter gives us a second coupon code.

**Behavior Noticed:**
- Coupon already used if you try to apply same coupon twice in a row
- This check is done only with the last used coupon, if we alternate it doesn't check the whole list.

**Tools Used:**
- Proxy, Repeater

---

## Exploitation Steps

1. Login, add jacket to cart
2. Sign up for newsletter, get new coupon
3. Use the 2 coupons alternatingly, and reduce the price to 0

---

## Fix Recommendations

- Check the whole list of coupons used instead of just the last coupon used for error.
