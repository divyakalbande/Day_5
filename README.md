# Day_5
---

# 🚢 Titanic Dataset Analysis

This analysis explores survival factors in the Titanic dataset, examining missing data, key distributions, and correlations to understand what influenced passenger survival. The goal is to extract actionable insights and inform future modeling steps.

---

## 🧩 Missing Data Overview

| Feature    | Missing Values | % Missing | Action Plan               |
|------------|----------------|-----------|---------------------------|
| `Cabin`    | 687            | 77.1%     | 🔥 Drop feature (too sparse) |
| `Age`      | 177            | 19.9%     | 🛠️ Impute median/mean       |
| `Embarked` | 2              | 0.2%      | ✅ Fill with mode ('S')     |

**Decisions:**
- `Cabin` dropped due to high sparsity.
- `Age` retained — imputation required due to its importance.
- `Embarked` missing values trivially imputed.

---

## 📊 Dataset Overview

### 🚨 Survival Rate
- **38.3% survived** (241/629)
- **Baseline accuracy** (predict all died): **61.7%**

---

## 🎯 Key Features & Observations

### 🏷️ Passenger Class (`Pclass`)
| Class | % of Passengers | Survival Rate |
|-------|------------------|----------------|
| 1st   | 24.2%           | 62.96%        |
| 2nd   | 20.7%           | 47.28%        |
| 3rd   | 55.1%           | 24.24%        |

**Insight**: Clear socioeconomic gradient — **higher class = higher survival**.

---

### 🚻 Gender (`Sex`)
| Gender | % of Passengers | Survival Rate |
|--------|------------------|----------------|
| Male   | ~65%             | 18.89%        |
| Female | ~35%             | 74.20%        |

**Insight**: "Women and children first" policy highly evident.

---

### 🎂 Age
- **Median Age**: 28 years
- **IQR**: 20–38 years
- **Distribution**: Right-skewed, possibly bimodal

**Insight**: 25% under 20, 25% over 38 — but age was **less predictive** than class/gender.

---

### 💰 Fare
- **Range**: $0–$512  
- **75% paid** < $50  
- **Distribution**: Highly right-skewed

**Insight**: High fares = higher class → better survival odds.

---

### 🛳️ Embarkation Port (`Embarked`)
| Port | % of Passengers | Survival Rate |
|------|------------------|----------------|
| S    | 72%             | 33.90%        |
| C    | 19%             | 55.36%        |
| Q    | 9%              | 38.96%        |

**Insight**: Embarked port correlated with class — **Cherbourg (C)** had wealthier passengers.

---

## 🕵️ Survival Factors Summary

| Feature      | High Survival Indicator       |
|--------------|-------------------------------|
| `Sex`        | Female                        |
| `Pclass`     | 1st Class                     |
| `Has_Cabin`  | Yes (proxy for class)         |
| `Embarked`   | Cherbourg (C)                 |
| `Fare`       | High fare                     |

**Worst Odds**: Male, 3rd class, no cabin, boarded at Southampton.

---

## 📈 Correlation with Survival (`Survived`)

| Feature     | Correlation | Insight                              |
|-------------|-------------|--------------------------------------|
| `Pclass`    | **-0.34**   | Strongest negative — lower class = lower survival |
| `Has_Cabin` | +0.32       | Strong positive — cabins = privilege |
| `Fare`      | +0.26       | Wealth mattered                     |
| `Age`       | -0.06       | Mild disadvantage for older passengers |
| `SibSp`     | -0.04       | Slight drop with larger family size |
| `Parch`     | +0.08       | Weak support for traveling with parents/children |

---

## ✅ Simplest Baseline Model

**Assumption**:  
- All **females survived**
- All **males perished**

**Accuracy**: **78.67%**

> Strong baseline, but combining gender, class, fare, and family features may yield better performance.

---

## 🧠 Final Takeaways

- **Class and gender dominate** survival outcomes.
- Wealth, inferred from fare and cabin presence, played a decisive role.
- Age and family presence were secondary but not insignificant.
- Baseline rule using just gender yields surprisingly strong accuracy.

---
