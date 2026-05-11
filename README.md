# SDR-Aggregate-Planning

## Overview
An Excel-based **Aggregate Planning model** using the **Search Decision Rule (SDR)** method to determine the optimal workforce level that minimizes total operational cost over a 6-month planning horizon.

## Problem Statement
Given monthly demand forecasts and a set of cost parameters, the model finds the optimal number of workers to deploy each month by iteratively testing candidate workforce configurations and accepting only those that reduce total cost.

### Demand Forecast (Jan–Jun)
| Month | Jan | Feb | Mar | Apr | May | Jun | Total |
|-------|-----|-----|-----|-----|-----|-----|-------|
| Demand (Units) | 1200 | 1500 | 1800 | 2100 | 1900 | 1600 | 10,100 |

## Cost Parameters
| Parameter | Symbol | Value | Unit |
|-----------|--------|-------|------|
| Production rate/worker | p | 30 | units/worker/month |
| Initial workforce | W₀ | 50 | workers |
| Initial inventory | I₀ | 200 | units |
| Hiring cost | Cₕ | ₹5,000 | per worker hired |
| Firing cost | Cf | ₹8,000 | per worker fired |
| Holding cost | Ch | ₹20 | per unit/month |
| Backorder cost | Cb | ₹50 | per unit/month |
| Labour cost/worker | Cw | ₹12,000 | per worker/month |

## Optimal Solution
- **Optimal Workforce:** W* = **55 workers** (Level Strategy)
- **Total Minimum Cost:** ₹ **40,33,500**

### Monthly Cost Summary
| Month | Labour Cost | Hire Cost | Fire Cost | Hold Cost | Back Cost | Monthly TC |
|-------|------------|-----------|-----------|-----------|-----------|------------|
| January | ₹6,60,000 | ₹25,000 | ₹0 | ₹13,000 | ₹0 | ₹6,98,000 |
| February | ₹6,60,000 | ₹0 | ₹0 | ₹16,000 | ₹0 | ₹6,76,000 |
| March | ₹6,60,000 | ₹0 | ₹0 | ₹13,000 | ₹0 | ₹6,73,000 |
| April | ₹6,60,000 | ₹0 | ₹0 | ₹4,000 | ₹0 | ₹6,64,000 |
| May | ₹6,60,000 | ₹0 | ₹0 | ₹0 | ₹2,500 | ₹6,62,500 |
| June | ₹6,60,000 | ₹0 | ₹0 | ₹0 | ₹0 | ₹6,60,000 |
| **TOTAL** | **₹39,60,000** | **₹25,000** | **₹0** | **₹46,000** | **₹2,500** | **₹40,33,500** |

## SDR Method — How It Works
The Search Decision Rule is a heuristic optimization technique:
1. Start with a baseline workforce level (Trial T1)
2. Test alternative configurations (perturbations of ±1 worker per period)
3. Accept a trial only if it reduces Total Cost below the current best
4. Stop (converge) when no single-variable perturbation improves the solution

**Convergence:** Algorithm stopped at Trial T10 — Level W=55 confirmed optimal at ₹40,33,500.

## Key Formulas
| Variable | Formula | Notes |
|----------|---------|-------|
| Production | Pt = Wt × 30 | 30 units per worker per month |
| ΔW | Wt − Wt₋₁ | Change in workforce |
| Hire | Ht = MAX(0, ΔW) | Only positive changes |
| Fire | Ft = MAX(0, −ΔW) | Only negative changes |
| Inventory | It = It₋₁ + Pt − Dt | Rolling balance |
| Holding Cost | MAX(0, It) × ₹20 | Only when inventory > 0 |
| Backorder Cost | MAX(0, −It) × ₹50 | Only when inventory < 0 |

## Workbook Structure
| Sheet | Description |
|-------|-------------|
| `1_Problem_Data` | Demand forecast and all cost/operational parameters with named ranges |
| `2_SDR_Optimal_Plan` | Step-by-step optimal plan with month-wise workforce and cost calculations |
| `3_SDR_Trial_Comparison` | All 10 SDR trials compared — accepted vs. rejected solutions |
| `4_Cost_Breakdown` | Complete cost breakdown with component-wise % analysis |
| `5_Inventory_Trace` | Month-wise inventory balance showing holding and backorder events |

## Key Insights
- **Labour cost dominates** at 98.18% of total cost — minimizing workforce churn is critical
- **Zero firings** achieved with the level strategy (W=55 constant)
- **Backorder occurs only in May** (50 units short) — lowest-cost tradeoff vs. overstaffing
- **Chase strategies (T3, T6) were significantly more expensive** due to high hiring/firing costs

## Tools Used
- Microsoft Excel (with named ranges and cross-sheet formula references)
- SDR heuristic optimization (manual iterative search)
- 
## Project File
`SDR_Aggregate_Planning.xlsx`

---

## Author
**Manish Tiwari**
M.Tech (Industrial Engineering), MNIT Jaipur
