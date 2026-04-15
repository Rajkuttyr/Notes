# 🏭 B3: Supply, Demand & Inventory Planning in Supply Chain Analytics
**Subject:** CCW331 – Business Analytics
**Topic:** Supply Chain Analytics
**Marks:** 10 | **Pages:** 3

---

> 💡 **Feynman Trick:** Imagine running a restaurant. You must know **how many customers will come** (demand), **how much food to order** (supply), and **how much to keep in the fridge** (inventory). Get any one wrong — you either waste food or disappoint customers. Supply Chain Analytics solves exactly this, but at a business scale of millions of products.

---

## 📌 1. Introduction / Definition

> **Supply Chain Analytics** is the application of data analysis and predictive modelling to optimize the flow of goods, services, and information from supplier to customer.

### Three Core Pillars:
```
SUPPLY PLANNING       DEMAND PLANNING       INVENTORY PLANNING
(What can we          (What do customers    (How much to stock
 produce/procure?)     need & when?)         & where?)
        \                   |                     /
         \                  |                    /
          ↓                 ↓                   ↓
              OPTIMIZED SUPPLY CHAIN
          (Right product, right place, right time, right cost)
```

---

## 📌 2. Step 1: Demand Planning

### 🧠 Feynman Explanation:
> Before you shop for groceries, you plan what meals you'll cook this week. You're doing demand planning. Businesses do the same — but for thousands of products across hundreds of locations.

### Definition:
> **Demand Planning** is the process of **forecasting future customer demand** for products or services using historical data, market trends, and analytical models.

### Steps in Demand Planning:
```
Step 1: Collect historical sales data (past 2–3 years)
Step 2: Identify patterns (seasonality, trends, events)
Step 3: Apply forecasting model (ARIMA, Random Forest)
Step 4: Adjust for external factors (promotions, economy)
Step 5: Generate demand forecast (weekly/monthly/quarterly)
Step 6: Share forecast with supply and inventory teams
```

### Demand Forecasting Methods:
| Method | Description | Example |
|--------|-------------|---------|
| **Moving Average** | Average of last N periods | 3-month average sales |
| **Exponential Smoothing** | More weight to recent data | Last month weighted more |
| **ARIMA** | Statistical time series model | Monthly demand trend |
| **ML Models** | Random Forest / XGBoost | Multi-variable demand |
| **Collaborative Forecasting** | Input from sales & marketing teams | Promotion-adjusted forecast |

### Key Metrics:
- **Forecast Accuracy** = (1 − MAPE) × 100%
- **Bias** = Systematic over/under forecasting

**Example:**
> Walmart uses ML-based demand forecasting to predict demand for 140,000+ products weekly, adjusting for weather, holidays, and local events. Result: 20% reduction in stockouts.

---

## 📌 3. Step 2: Supply Planning

### 🧠 Feynman Explanation:
> After deciding you need 100 pizzas for the weekend (demand), you now plan: How much flour, tomato, and cheese to order? From which supplier? By when? That's supply planning.

### Definition:
> **Supply Planning** determines **how to source, produce, or procure** the right quantity of goods to meet the forecasted demand within cost and time constraints.

### Steps in Supply Planning:
```
Step 1: Receive demand forecast from demand planning team
Step 2: Assess current inventory levels & production capacity
Step 3: Identify supply gaps (demand > supply = shortage risk)
Step 4: Select optimal suppliers (cost, lead time, reliability)
Step 5: Create purchase/production orders
Step 6: Monitor supplier performance & adjust plans
```

### Supply Planning Analytics:
| Analytics Type | Purpose |
|----------------|---------|
| **Supplier Scorecards** | Rate suppliers on cost, quality, on-time delivery |
| **Lead Time Analysis** | Predict supplier delivery time variability |
| **Capacity Planning** | Match production capacity to demand |
| **Risk Analytics** | Identify single-source supplier risks |
| **Cost Optimization** | Find cheapest sourcing combination |

**Example:**
> Apple uses supply analytics to manage 200+ suppliers globally, predicting lead times and qualifying backup suppliers to prevent production disruption.

---

## 📌 4. Step 3: Inventory Planning

### 🧠 Feynman Explanation:
> Your fridge has limited space. Too many vegetables → some will rot. Too few → you run out mid-week. Inventory planning finds the **perfect balance** — just enough stock, at the right time, in the right location.

### Definition:
> **Inventory Planning** determines the **optimal quantity of stock** to maintain at each location to fulfill demand while minimizing holding costs and preventing stockouts.

### Key Concepts:
```
Reorder Point (ROP) = Average Daily Demand × Lead Time + Safety Stock

Safety Stock = Z × σ × √Lead Time
(Buffer stock to cover demand uncertainty)

Economic Order Quantity (EOQ) = √(2DS/H)
D = Annual demand
S = Ordering cost per order
H = Holding cost per unit per year
```

### Inventory Analytics Steps:
```
Step 1: Classify inventory (ABC Analysis)
         A = High value, low volume → tight control
         B = Medium value & volume → moderate control
         C = Low value, high volume → minimal control

Step 2: Calculate safety stock levels

Step 3: Set reorder points (trigger auto-ordering)

Step 4: Optimize order quantities (EOQ)

Step 5: Monitor inventory turnover ratio

Step 6: Identify slow-moving / dead stock
```

### Inventory KPIs:
| KPI | Formula | Target |
|-----|---------|--------|
| **Inventory Turnover** | COGS ÷ Avg Inventory | Higher = better |
| **Days Sales of Inventory** | (Avg Inventory ÷ COGS) × 365 | Lower = better |
| **Fill Rate** | Orders fulfilled ÷ Total orders × 100 | > 95% |
| **Carrying Cost %** | Holding cost ÷ Inventory value × 100 | 20–30% typical |

**Example:**
> Amazon's inventory analytics system automatically calculates reorder points for millions of SKUs and triggers purchase orders without human intervention, maintaining a fill rate above 99%.

---

## 📌 5. Integrated Supply Chain Analytics Diagram

```
SUPPLIERS
    ↓  (Supply Analytics: lead time, cost, risk)
PROCUREMENT
    ↓  (Purchase orders based on demand forecast)
WAREHOUSE / INVENTORY
    ↓  (Inventory Analytics: ABC, EOQ, Safety Stock)
DISTRIBUTION
    ↓  (Logistics Analytics: route optimization)
CUSTOMER
    ↑  (Demand Analytics feeds back into planning)
```

---

## 📌 6. Real-World Application – FMCG Company

| Phase | Analytics Used | Outcome |
|-------|---------------|---------|
| Demand Planning | ML demand forecasting | 15% forecast accuracy improvement |
| Supply Planning | Supplier scorecards | 10% cost reduction |
| Inventory Planning | ABC + EOQ + safety stock | 25% reduction in excess inventory |
| Logistics | Route optimization | 18% fuel cost reduction |
| Overall | Integrated dashboard | Real-time supply chain visibility |

---

## 📌 7. Advantages and Disadvantages

### ✅ Advantages
1. **Reduces waste** – Prevents overstocking and product expiry.
2. **Prevents stockouts** – Safety stock and reorder points ensure availability.
3. **Cost savings** – Optimized ordering reduces procurement and holding costs.
4. **Faster response** – Analytics enables quick reaction to demand changes.
5. **Data-driven decisions** – Replaces gut-feeling decisions with evidence-based planning.

### ❌ Disadvantages
1. **Data quality dependency** – Inaccurate historical data leads to poor forecasts.
2. **Integration complexity** – Supply chain spans multiple systems; data silos are common.
3. **Demand uncertainty** – Black swan events (COVID, natural disasters) disrupt all models.
4. **Implementation cost** – Analytics platforms and skilled analysts are expensive.

---

## 📌 8. Conclusion

> Supply Chain Analytics integrates **demand planning, supply planning, and inventory optimization** into a seamless data-driven process that ensures the right product is in the right place at the right time.

- **Demand planning** uses forecasting models to predict customer needs.
- **Supply planning** ensures procurement and production match demand.
- **Inventory planning** maintains optimal stock levels using EOQ and safety stock.

> Together, these create a **resilient, efficient, and cost-optimized** supply chain.

> 🎯 **Exam Tip:** Draw the integrated supply chain diagram, explain EOQ and ABC analysis, give the Walmart or Amazon example, and list KPIs for each phase.

---
*Tags: #BusinessAnalytics #CCW331 #SupplyChain #DemandPlanning #InventoryPlanning #EOQ #SafetyStock #Forecasting*
