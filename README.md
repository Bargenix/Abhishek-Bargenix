#first prompt
Sample Data Reference:
{
    "Live_data_from_frontend": """
    User Info:
    user_name = Anika, email = anika@gmail.com, orders = 12, spent = 1543, 
    refunds = 595, days_since_last = 228
    Product Info:
    product_name = Toe Ring, product_description = Simple metal toe rings..., 
    product_price = 706 INR, min_price_client = 367 INR, avg_inventory = 27
    """,
    "user": "User: 10% is less it seems is that all you can offer,ok lets say if you can make it to 25 thats a deal",
    "metadata": {
        "user_score": 21.55,
        "bargain_score": 40,
        "system_max_discount": 24.0,
        "current_round": 2,
        "previous_round_discount_given": 10
    }
}
# Basic Negotiation Prompt

## Overview
Handles immediate price negotiation with focus on current round decision-making.

## Data Structure
1. Parameter Summary:
   - Orders (12) → Impact on discount
   - Total Spent (₹1543) → Customer value
   - Days Since Last (228) → Engagement metric
   - Refunds (₹595) → Risk factor

2. User Profile Section:
   - Basic metrics
   - Verification status
   - Purchase history

3. Product Details:
   - Current price (₹706)
   - Minimum price (₹367)
   - Inventory level (27)

4. Negotiation State:
   - Current round (2/5)
   - Previous offer (10%)
   - User request (25%)
   - Maximum allowed (24%)

## Usage Example
context = {
    'orders': 12,
    'spent': 1543,
    'product_price': 706,
    'current_round': 2,
    'previous_round_discount_given': 10
}

messages = get_messages(context)
Output:
Bot: How about 15% off, making it ₹600.1? I'm open to hearing your offer too!


##second prompt

2. Second Prompt (Discount Calculation Framework)
# Discount Calculation Framework

## Overview
Detailed analysis framework for calculating optimal discount progression.

## Data Structure
1. Scenario Analysis:

User Profile:
- Orders: 12 (Medium)
- Total Spent: ₹1543 (Medium)
- Refund Rate: 38.6% (High risk)
- Last Active: 228 days (Inactive)
- Bargain Score: 40/100 (Average)

Product Status:
- Price: ₹706
- Min Price: ₹367 (52% of original)
- Inventory: 27 units (Normal)
##Decision Factors:
A. User Value (Score: 21.55/45)
- Tier: Medium
- Adjustment: 1.0-1.5%

B. Inventory Status (27 units)
- Level: Normal
- Adjustment: 0.5-1%

C. Product Age (183 days)
- Category: Old
- Adjustment: 1-2%
##Discount Progression:
Current Round (2/5):
- Base: 10%
- New Offer: 15%
- Price: ₹600.1

Future Rounds:
Round 3: 19%
Round 4: 21%
Round 5: 24%

##Usage Example
context = {
    'user_score': 21.55,
    'inventory': 27,
    'product_age': 183,
    'current_round': 2,
    'max_rounds': 5
}

response = generate_discount_response(context)
Output Format:
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
    "system_max": 24%,
    "current_round": "2/5"
  }
}

##Third Prompt (Advanced Negotiation)
# Advanced Negotiation Prompt

## Overview
Comprehensive negotiation strategy with real-time metric calculation.

## Data Structure
1. User Metrics:
USER PROFILE
- Orders: 12 (User Score: 21.55)
- Total Spent: ₹1,543 (Refund Rate: 38.6%)
- Bargain Skill: 40/100
- Days Since Last: 228
Product Analysis:
PRODUCT STATUS
- Price: ₹706 (Min: ₹367 = 52%)
- Inventory: 27 units
- Age: 183 days
- Score: 18.70

##Negotiation Parameters:
NEGOTIATION STATE
- Round: 2/5
- Last Offer: 10% (₹635.4)
- User Request: 25%
- System Max: 24%

  ##Calculation Factors:
  DISCOUNT FACTORS
1. User Value (21.55/45)
   - Tier: Medium
   - Impact: 1.0x base

2. Inventory (27 units)
   - Level: Normal
   - Adjustment: 0.5%

3. Product Age (183 days)
   - Category: Old
   - Adjustment: 1%

4. Bargain Score (40/100)
   - Level: Average
   - Impact: 1.0x base

5. Round Progression
   - Current: 2/5
   - Expected Increase: 2%
  Usage Example
context = {
    'user_score': 21.55,
    'spent': 1543,
    'refunds': 595,
    'product_price': 706,
    'current_round': 2,
    'previous_round_discount_given': 10
}

messages = get_messages(context)

Output Format
Detailed response with:
- Calculated metrics
- Strategic recommendation
- Factor-based adjustments

