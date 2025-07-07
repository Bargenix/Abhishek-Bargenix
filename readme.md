# 🧠 AI-Powered Price Negotiation Framework

This repository showcases an advanced **LLM-based price negotiation framework**. It combines real-time user data, product status, and dynamic discount strategies to simulate intelligent bargaining experiences between an AI chatbot and customers.

---

## 📦 Sample Data Reference

```json
{
  "Live_data_from_frontend": "User Info: user_name = Anika, email = anika@gmail.com, orders = 12, spent = 1543, refunds = 595, days_since_last = 228\nProduct Info: product_name = Toe Ring, product_description = Simple metal toe rings..., product_price = 706 INR, min_price_client = 367 INR, avg_inventory = 27",
  "user": "User: 10% is less it seems is that all you can offer, ok lets say if you can make it to 25 thats a deal",
  "metadata": {
    "user_score": 21.55,
    "bargain_score": 40,
    "system_max_discount": 24.0,
    "current_round": 2,
    "previous_round_discount_given": 10
  }
}
```

---

## 🧹 Prompt 1: Basic Negotiation Prompt

### 🔍 Overview

Handles immediate price negotiation, with a focus on **current-round decision-making** based on limited user and product data.

### 🧱 Data Structure

- **User Metrics**

  - Orders: `12`
  - Spent: `₹1543`
  - Days Since Last Purchase: `228`
  - Refunds: `₹595`

- **Product Details**

  - Product Price: `₹706`
  - Minimum Price (Client Threshold): `₹367`
  - Inventory: `27 units`

- **Negotiation State**

  - Current Round: `2/5`
  - Previous Discount: `10%`
  - User Request: `25%`
  - System Max: `24%`

### 💬 Usage Example

```python
context = {
    'orders': 12,
    'spent': 1543,
    'product_price': 706,
    'current_round': 2,
    'previous_round_discount_given': 10
}

messages = get_messages(context)
```

**Output:**

```
Bot: How about 15% off, making it ₹600.1? I'm open to hearing your offer too!
```

---

## 📊 Prompt 2: Discount Calculation Framework

### 🔍 Overview

A detailed analysis framework for calculating **progressive discounts** based on risk, user value, and product status.

### 🧱 Data Structure

#### 🧑‍💼 User Profile

- Orders: `12` (Medium)
- Spent: `₹1543` (Medium)
- Refund Rate: `38.6%` (High Risk)
- Inactivity: `228 days`
- Bargain Score: `40/100` (Average)

#### 🛆 Product Status

- Price: `₹706`
- Minimum: `₹367` (52% of base)
- Inventory: `27` units (Normal)
- Age: `183 days`

### 📊 Decision Factors

| Factor      | Level  | Adjustment |
| ----------- | ------ | ---------- |
| User Value  | Medium | +1.0–1.5%  |
| Inventory   | Normal | +0.5–1%    |
| Product Age | Old    | +1–2%      |

---

### 📈 Discount Progression

| Round | Discount | Final Price (INR) |
| ----- | -------- | ----------------- |
| 2     | 15%      | ₹600.10           |
| 3     | 19%      | ₹571.86           |
| 4     | 21%      | ₹557.74           |
| 5     | 24%      | ₹536.56           |

### 🧺 Usage Example

```python
context = {
    'user_score': 21.55,
    'inventory': 27,
    'product_age': 183,
    'current_round': 2,
    'max_rounds': 5
}
```

**Output:**

```json
{
  "discount_progression": {
    "round_2": "15% (₹600.1)",
    "round_3": "19% (₹571.86)",
    "round_4": "21% (₹557.74)",
    "round_5": "24% (₹536.56)"
  },
  "reasoning": "Gradual increase based on user value (medium) and inventory status (normal)",
  "constraints": {
    "min_price": 367,
    "system_max": 24,
    "current_round": "2/5"
  }
}
```

---

## 🌟 Prompt 3: Advanced Negotiation Strategy

### 🔍 Overview

An in-depth, **factor-driven negotiation model** with dynamic strategy recommendations based on user risk, product conditions, and historical context.

### 🧱 Data Structure

#### 👤 User Profile

- Orders: `12` (User Score: `21.55`)
- Total Spent: `₹1543`
- Refund Rate: `38.6%`
- Bargain Skill: `40/100`
- Days Since Last Purchase: `228`

#### 🛅 Product Status

- Current Price: `₹706`
- Minimum: `₹367` (52%)
- Inventory: `27`
- Age: `183 days`
- Product Score: `18.70`

---

### 📌 Negotiation Parameters

- Round: `2/5`
- Last Offer: `10%` → `₹635.4`
- User Request: `25%`
- System Max: `24%`

---

### 🧠 Discount Factors Breakdown

| Factor          | Detail            | Adjustment        |
| --------------- | ----------------- | ----------------- |
| User Value      | Medium (21.55/45) | ×1.0 base         |
| Inventory Level | Normal (27)       | +0.5%             |
| Product Age     | Old (183 days)    | +1%               |
| Bargain Score   | Average (40/100)  | ×1.0 base         |
| Round Progress  | 2/5               | +2% expected bump |

---

### 🧺 Usage Example

```python
context = {
    'user_score': 21.55,
    'spent': 1543,
    'refunds': 595,
    'product_price': 706,
    'current_round': 2,
    'previous_round_discount_given': 10
}
```

**Expected Output:**

- Strategic offer recommendation
- Justification based on current metrics
- Future discount outlook

---

## 📚 Conclusion

This system simulates a **real-time AI-based negotiation engine**. It helps businesses optimize:

- Revenue retention
- Customer satisfaction
- Inventory clearance

By integrating contextual and behavioral data, it can power intelligent **conversational commerce bots**.

---

