# PRPL Data Cleaning Documentation

---

## Introduction

After inserting the main data of products, their costs, and quantities, the next step was to clean and structure the dataset so that it could support profitability and pricing analysis. This document explains the transformations, calculated fields, and indicators created during the cleaning process.

> **Note:** *(Insert image: snapshot of raw Excel table before cleaning)*

---

## Goal Margin Setup

* Stakeholders provided a **goal margin of 0.5 (50%)**.
* This value was placed in a dedicated cell, allowing for dynamic adjustments in case the target changes.
* A supporting table was created to calculate **trip expenses** (e.g., travel, shipping, hotel) and to sum up the **total quantity of goods**.

> **Note:** *(Insert image: small table of expenses and quantities)*

---

## Column Additions and Calculations

### 1. **Unit Cost After Expenses**

Formula:

```
Unit Cost + (Total Expenses / Total Number of Items)
```

This adjusts the base unit cost to include a share of total expenses.

### 2. **Goal Unit Price**

Formula:

```
Unit Cost After Expenses / (1 – Goal Margin)
```

Calculates the price at which a unit should be sold to achieve the goal margin.

### 3. **Goal Unit Profit**

Captures the profit per unit based on the calculated goal unit price.

---

### 4. **Actual Unit Prices**

* **Actual Unit Price (Main):** The initial price set by stakeholders before any discount.
* **Actual Unit Price (Lowest):** The lowest possible selling price after discounting/bargaining.
* **Actual Unit Price (Average):** Weighted average between main and lowest prices, based on the assumption:

  * 80% of items sold at the lowest price
  * 20% of items sold at the main price

Formula:

```
=(0.8 * [Actual Unit Price (Lowest)]) + (0.2 * [Actual Unit Price (Main)])
```

* **Actual Unit Profit (Average):** Profit per unit at the average selling price.

---

### 5. **Aggregate Calculations**

* **Total Price of Articles (Average):**
  Potential total revenue from all units of a given article.

* **Total Profit of Articles (Average):**
  Potential profit from all units of a given article.

Both use the **Actual Unit Price (Average)** in their calculations.

> **Note:** *(Insert image: cleaned Excel table with calculated columns)*

---

## Indicators

### 1. **Actual vs. Goal Sales Ratio (Based on Margin)**

Formula:

```
(Total of Actual Sales) ÷ (Total of Goal Sales)
```

Where:

* *Actual Sales* = sum of actual sales prices across all items
* *Goal Sales* = sum of (goal price × quantity) for each item

### 2. **Actual Margin**

Formula:

```
(Revenue – Cost) / Revenue
```

Indicates the real margin achieved based on actual prices.

### 3. **% of Goal Margin Achieved**

Formula:

```
Actual Margin ÷ Target Margin
```

Measures how close the actual results are to the intended profitability goal.

### 4. **Markup**

Formula:

```
Actual Margin / (1 – Actual Margin)
```

Represents the revenue percentage added above cost.

> **Note:** *(Insert image: dashboard of margin and ratio indicators)*

---

## Conclusion

The data cleaning process transformed raw invoice and expense data into a structured dataset ready for analysis. By systematically calculating adjusted costs, goal prices, and key profitability indicators, PRPL was able to evaluate its current performance against its target margin and make data-driven pricing decisions.
