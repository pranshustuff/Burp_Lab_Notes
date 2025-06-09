
# 🧪 Burp Lab Note: *Insufficient workflow validation*

## 🔹 Lab Metadata
- **Title**: Insufficient workflow validation
- **Category**: Business Logic
- **Difficulty**: Practitioner

---

## 🧠 Goal
> _Buy an item (Leather Jacket) from shop without enough store credits for said item through your account._

---

## 🛠️ Setup & Observations
- **Initial Recon**: Tried adding -1 of the item, tried various outputs in the coupon area, used repeater to change workflow order.
- **Burp Tools Used**: Proxy & Repeater
- **Assumed workflow**: Users logs in -> puts item in cart -> users goes to cart -> user checks out and store checks at the time  if user has enough balance.
- **Interesting Requests/Responses**:
  - Endpoint: `POST /cart
  - Request: Added some cheap item clicked checkout and then added jacket through repeater in POST /cart
  - Response: returned `Insufficient funds`

---

## 🐞 Vulnerability Analysis
- **Vuln Type**: Business Logic
- **Injection Point**: POST /cart
- **Indicators**:
  - GET /cart?err=INSUFFICIENT_FUNDS request if clicked checkout after jacket in cart.

---

## 🔓 Exploitation Steps
1. Added cheap item to cart and clicked checkout with intercept.
2. Forwarded the POST /cart/checkout request, recieved /GET /cart/order-confirmation?order-confirmed=true
3. Added jacket to cart through repeater while the above GET is intercepted
4. Forwarded the GET /cart/order-confirmation?order-confirmed=true
5. Site ordered both cheap item and jacket.

---

## 🔐 Fix Recommendations (Optional)
- Maybe check for items in cart in the GET request also.

---

## ✍️ Notes & Takeaways
- Really cool. I learned that repeater can still interact with the site while requests are intercepted. Can use in further labs.
- Learned worklow validation.
