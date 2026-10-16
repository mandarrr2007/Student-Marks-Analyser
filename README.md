# 🎓 Student Marks Performance Analyzer

A structured NumPy analysis project demonstrating core array manipulation, multi-dimensional slicing, conditional boolean masking, and statistical evaluation on academic datasets.

This project is fully implemented and interactive in the notebook:
👉 **[student_marks_analyzer.ipynb](student_marks_analyzer.ipynb)** (open directly in Jupyter or Google Colab).

---

## 📌 Project Overview

This project models and analyzes examination data for **50 students across 5 subjects**:
- **Mathematics**
- **Physics**
- **Chemistry**
- **English**
- **Computer Science**

The data is represented as a 2-dimensional NumPy matrix of shape `(50, 5)` containing generated integer scores in the range `[35, 100)`.

---

## 🧠 NumPy Concepts Covered

| Concept | Implementation in [student_marks_analyzer.ipynb](student_marks_analyzer.ipynb) | Purpose |
| :--- | :--- | :--- |
| **Array Initialization** | `np.array([...])`, `np.random.randint(35, 100, (50, 5))` | Creating subject labels and student mark matrix |
| **Array Attributes** | `marks.shape`, `marks.ndim`, `marks.size`, `marks.dtype` | Inspecting dimensions, axes, element count, and type |
| **Basic & Negative Indexing** | `marks[0, 2]`, `marks[:, -1]` | Direct access to individual student scores and last column |
| **2D Slicing** | `marks[:10, :]`, `marks[:, 0:3]`, `marks[20:25, 1:4]` | Extracting student subsets and subject blocks |
| **Boolean Masking** | `marks < 40`, `marks > 90`, `(avg >= 80) & (avg < 90)` | Conditional filtering for failures, distinctions & grade bands |
| **Aggregation & Reduction** | `np.mean(axis=0/1)`, `np.max()`, `np.sum()`, `np.argmax()` | Calculating averages, toppers, and pass percentages |

---

## 🚀 Workflow & Notebook Structure

The notebook [student_marks_analyzer.ipynb](student_marks_analyzer.ipynb) is organized into 5 progressive steps:

### 1. Data Initialization
Creates a 1D array of subject names and initializes a `(50, 5)` matrix of random marks:
```python
import numpy as np

np.random.seed(42)  # For reproducible analysis
subjects = np.array(['Mathematics', 'Physics', 'Chemistry', 'English', 'Computer Science'])
marks = np.random.randint(35, 100, size=(50, 5))
```

### 2. Attribute Inspection
Evaluates key metadata attributes of the marks matrix:
```python
print(marks.shape)  # (50, 5) -> 50 students x 5 subjects
print(marks.ndim)   # 2 -> 2-dimensional matrix
print(marks.size)   # 250 -> Total score data points
print(marks.dtype)  # int64 -> Integer data type
```

### 3. Indexing and 2D Slicing
Demonstrates multi-axis data extraction:
- **First 10 students:** `marks[:10, :]`
- **Last subject (negative indexing):** `marks[:, -1]`
- **STEM Subjects (columns 0 to 2):** `marks[:, 0:3]`
- **Sub-cohort matrix:** `marks[20:25, 1:4]`

### 4. Boolean Masking & Grade Classification
Applies vectorized boolean logic:
- **Failing scores (< 40):** `fail_mask = marks < 40`
- **Students with at least 1 fail:** `np.any(fail_mask, axis=1)`
- **Distinctions (> 90):** `distinction_mask = marks > 90`
- **Grade Bands:**
  - `A+` : `Average >= 90`
  - `A`  : `80 <= Average < 90`
  - `B`  : `70 <= Average < 80`
  - `C`  : `60 <= Average < 70`
  - `D`  : `40 <= Average < 60`
  - `F`  : `Average < 40`

### 5. Subject-wise Analysis & Toppers
Calculates metrics per subject (along `axis=0`) and overall student metrics (along `axis=1`):
- **Subject Averages:** `np.mean(marks, axis=0)`
- **Subject Toppers:** `np.where(marks[:, i] == np.max(marks[:, i]))[0]`
- **Pass Percentage:** `(np.sum(marks >= 40, axis=0) / 50) * 100`
- **Overall Class Topper:** `np.argmax(np.sum(marks, axis=1))`
- **All-Subject Pass Rate:** `np.all(marks >= 40, axis=1)`

---

## 📊 Sample Output Summary

```text
======================================================================
Subject            |    Avg |  Max | Topper ID(s)   |  Pass % | Passed
----------------------------------------------------------------------
Mathematics        |  65.50 |   97 | #11            |   86.0% |  43/50
Physics            |  65.74 |   99 | #19            |   88.0% |  44/50
Chemistry          |  68.20 |   98 | #2             |   94.0% |  47/50
English            |  66.30 |   99 | #14            |   84.0% |  42/50
Computer Science   |  68.78 |   98 | #5, #48        |   90.0% |  45/50
======================================================================

🏆 Overall Class Topper : Student #5 (Score: 449/500, Average: 89.80%)
🎓 All-Subject Pass Rate: 29/50 students (58.0% passed all 5 subjects)
```

---

## 📁 Dataset Reference: `student_marks.csv`

The generated dataset is exported in **[student_marks.csv](student_marks.csv)** containing:
- `Student_ID`: Unique student identifier (`Student_01` to `Student_50`)
- `Mathematics`, `Physics`, `Chemistry`, `English`, `Computer_Science`: Subject scores
- `Total_Marks`: Aggregate score out of 500
- `Average`: Percentage / mean score
- `Grade`: Performance grade (`A+`, `A`, `B`, `C`, `D`, `F`)
- `Status`: Final qualification status (`Pass` if all subjects >= 40, else `Fail`)

### Loading Dataset in NumPy:
```python
import numpy as np

# Load only marks matrix (columns 1 to 5) skipping the header row
marks_from_csv = np.genfromtxt('student_marks.csv', delimiter=',', skip_header=1, usecols=(1, 2, 3, 4, 5))
print("Loaded marks shape:", marks_from_csv.shape)  # (50, 5)
```

---

## 💻 How to Run

### Running in Google Colab / Jupyter
1. Open or upload **[student_marks_analyzer.ipynb](student_marks_analyzer.ipynb)** into [Google Colab](https://colab.research.google.com/) or your local Jupyter environment.
2. Run each cell sequentially using `Shift + Enter` or select **Runtime > Run all**.
3. All outputs, boolean mask filters, grade distributions, and topper statistics will be generated interactively.
