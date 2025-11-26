Sure! Let’s go **step by step** in **easy language**.

---

### **Given dataset (example)**

Suppose we have this small dataset:

[
\text{Data: } 4, 8, 6, 5, 3, 4, 7
]

---

## **1. Mean (Average)**

The **mean** is the sum of all values divided by the number of values.

[
\text{Mean} = \frac{\text{Sum of all values}}{\text{Number of values}}
]

**Step-by-step:**

[
\text{Sum} = 4 + 8 + 6 + 5 + 3 + 4 + 7 = 37
]
Number of values = 7

[
\text{Mean} = \frac{37}{7} \approx 5.29
]

✅ **When to use:**

* Use mean when data is **continuous** and **no extreme outliers**.
* It gives a **central value**.

---

## **2. Median**

The **median** is the middle value when data is arranged in **ascending order**.

**Step 1:** Arrange data:
[
3, 4, 4, 5, 6, 7, 8
]

**Step 2:** Find the middle value (for odd number of values, it’s the center).

* Middle value = 5

✅ **Median = 5**

**When to use:**

* Use median when data has **outliers** or is **skewed**.
* It is **not affected by extreme values**.

---

## **3. Mode**

The **mode** is the value that **appears most frequently**.

* In our dataset: 4 appears **twice**, others appear **once**.

✅ **Mode = 4**

**When to use:**

* Use mode for **categorical data** or when you want to know the **most common value**.

---

## **4. Standard Deviation (SD)**

The **standard deviation** measures how much the data **varies from the mean**.

**Step 1:** Find differences from mean and square them.

[
x - \bar{x} \text{ (difference)}, \quad (x - \bar{x})^2
]

| x | x - mean | (x - mean)² |
| - | -------- | ----------- |
| 4 | -1.29    | 1.6641      |
| 8 | 2.71     | 7.3441      |
| 6 | 0.71     | 0.5041      |
| 5 | -0.29    | 0.0841      |
| 3 | -2.29    | 5.2441      |
| 4 | -1.29    | 1.6641      |
| 7 | 1.71     | 2.9241      |

**Step 2:** Find variance (average of squared differences):

[
\text{Variance} = \frac{\text{Sum of squares}}{n} = \frac{19.4286}{7} \approx 2.7769
]

**Step 3:** Take square root to get SD:

[
\text{SD} = \sqrt{2.7769} \approx 1.67
]

✅ **When to use:**

* Use SD to understand **spread/dispersion** of data.
* Larger SD → data is more spread out.
* Smaller SD → data is closer to the mean.

---

### **Summary Table**

| Measure | Value | Best for                              |
| ------- | ----- | ------------------------------------- |
| Mean    | 5.29  | Symmetric data without outliers       |
| Median  | 5     | Skewed data or with outliers          |
| Mode    | 4     | Most frequent value, categorical data |
| SD      | 1.67  | Understanding spread/variability      |

---

If you want, I can **also show a quick Python code** to calculate all four measures instantly for any dataset.

Do you want me to do that?


Here’s a clear, easy-to-understand explanation:

---

## **1. Difference between Errors and Artefacts in Data Cleaning**

| **Aspect**            | **Errors**                                                         | **Artefacts**                                                                                                |
| --------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Definition**        | Mistakes in data that are **incorrect values** or inconsistencies. | Patterns or anomalies in data that are **not real**, often caused by data collection or measurement process. |
| **Example**           | A person’s age recorded as 250 years, or “M” instead of “Male”.    | Noise in a sensor reading, e.g., extra spikes in temperature due to faulty equipment.                        |
| **Cause**             | Human error, data entry mistakes, system bugs.                     | Instrument limitations, environmental factors, or measurement errors.                                        |
| **Focus in cleaning** | Correct or remove wrong values.                                    | Detect and remove spurious patterns that don’t reflect reality.                                              |

✅ **In short:**

* **Errors** = incorrect values.
* **Artefacts** = misleading patterns caused by measurement or process, not actual errors in data.

---

## **2. Two Imputation Techniques**

When data is **missing**, we often use imputation to fill it with reasonable values.

### **a) Mean/Median Imputation**

* **Idea:** Replace missing values with the **mean or median** of the available data for that feature.
* **Example:**

Dataset: 5, 7, NA, 8, 6

* Mean = (5+7+8+6)/4 = 6.5
* Replace NA with 6.5 → 5, 7, **6.5**, 8, 6

✅ **Pros:** Simple, fast
⚠️ **Cons:** Can reduce variability and affect distribution

**Tip:** Use **median** if data is skewed or has outliers.

---

### **b) k-Nearest Neighbors (KNN) Imputation**

* **Idea:** Fill missing values using the **values from the most similar data points** (neighbors).

* **Steps:**

  1. Identify rows with missing values.
  2. Find `k` nearest rows based on other features.
  3. Replace missing value with **average (numerical)** or **mode (categorical)** of neighbors.

* **Example:** Missing weight for person A → take average weight of 3 closest people in height, age, etc.

✅ **Pros:** Considers correlation between features, more accurate than mean/median
⚠️ **Cons:** Slower for large datasets

---

**Summary:**

| Imputation Technique | When to Use                                  |
| -------------------- | -------------------------------------------- |
| Mean/Median          | Small datasets, simple, numerical features   |
| KNN                  | Large datasets, when features are correlated |

---

If you want, I can also make a **super simple diagram showing Errors vs Artefacts and imputation methods** so it’s easier to remember for exams.

Do you want me to make that diagram?
