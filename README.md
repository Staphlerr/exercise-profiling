# Tutorial 5

Name: Belva Ghani Abhinaya

Class: Advance Programming B

Student Number: 2306203526

<details>
<summary><b>Performance Testing Results</b></summary>

## 1. Performance Testing Results

### Test Plan 1: /all-student

#### View Results Tree
![view-results all-student.jpg](screenshots/view-results%20all-student.jpg)

#### View Results In Table
![view-results-in-table all-student.jpg](screenshots/view-results-in-table%20all-student.jpg)

#### Summary Report
![summary-report all-student.jpg](screenshots/summary-report%20all-student.jpg)

#### Graph Results
![graph-results all-student.jpg](screenshots/graph-results%20all-student.jpg)

#### CLI Test
![cli-test all-student.jpg](screenshots/cli-test%20all-student.jpg)

### Test Plan 2: /all-student-name

#### View Results Tree
![view-results-tree all-student-name.jpg](screenshots/view-results-tree%20all-student-name.jpg)

#### View Results In Table
![view-results-in-table all-student-name.jpg](screenshots/view-results-in-table%20all-student-name.jpg)

#### Summary Report
![summary-report all-student-name.jpg](screenshots/summary-report%20all-student-name.jpg)

#### Graph Results
![graph-results all-student-name.jpg](screenshots/graph-results%20all-student-name.jpg)

#### CLI Test
![cli-test all-student-name.jpg](screenshots/cli-test%20all-student-name.jpg)

### Test Plan 3: /highest-gpa

#### View Results Tree
![view-result-tree highest-gpa.jpg](screenshots/view-result-tree%20highest-gpa.jpg)

#### View Results In Table
![view-result-in-table highest-gpa.jpg](screenshots/view-result-in-table%20highest-gpa.jpg)

#### Summary Report
![summary-report highest-gpa.jpg](screenshots/summary-report%20highest-gpa.jpg)

#### Graph Results
![graph-results highest-gpa.jpg](screenshots/graph-results%20highest-gpa.jpg)

#### CLI Test
![cli-test highest-gpa.jpg](screenshots/cli-test%20highest-gpa.jpg)

</details>

<details>
<summary><b>Profiling and Performance Optimization</b></summary>

## 2. Profiling and Performance Optimization Results

### 1. JMeter Test Results (Before vs After Optimization)

#### 1.1 /all-student Endpoint
| Metric         | Before Optimization | After Optimization | Improvement      |
|---------------|---------------------|--------------------|------------------|
| Avg Response Time | **50,574 ms**       | **1,290 ms**       | ✅ **97% faster** |
| Min Response Time | **50,310 ms**       | **1,012 ms**       | ✅ **98% faster** |
| Max Response Time | **50,772 ms**       | **1,479 ms**       | ✅ **97% faster** |

**Before Optimization:**  
![CLI Test Before - all-student](screenshots/cli-test all-student.jpg)

**After Optimization:**  
![CLI Test After - all-student](screenshots/cli-test all-student-after.jpg)

**Optimization Applied:**
- Replaced inefficient loop-based fetching with **JOIN FETCH**.
- Eliminated **N+1 query problem**.
- Reduced database calls drastically.

---

#### 1.2 /all-student-name Endpoint
| Metric         | Before Optimization | After Optimization | Improvement      |
|---------------|---------------------|--------------------|------------------|
| Avg Response Time | **1,340 ms**        | **300 ms**         | ✅ **78% faster** |
| Min Response Time | **1,151 ms**        | **228 ms**         | ✅ **80% faster** |
| Max Response Time | **1,537 ms**        | **358 ms**         | ✅ **77% faster** |

**Before Optimization:**  
![CLI Test Before - all-student-name](screenshots/cli-test all-student-name.jpg)

**After Optimization:**  
![CLI Test After - all-student-name](screenshots/cli-test all-student-name-after.jpg)

**Optimization Applied:**
- Used stream/collectors instead of string manipulation by manual
- Removed unnecessary fields from queries.
- Reduced memory usage by fetching only names.

---

#### **3.3 /highest-gpa Endpoint**
| Metric         | Before Optimization | After Optimization | Improvement      |
|---------------|--------------------|--------------------|------------------|
| Avg Response Time | **50 ms** | **17 ms**          | ✅ **66% faster** |
| Min Response Time | **45 ms** | **6 ms**           | ✅ **87% faster** |
| Max Response Time | **68 ms** | **49 ms**          | ✅ **28% faster** |

**Before Optimization:**  
![CLI Test Before - highest-gpa](screenshots/cli-test highest-gpa.jpg)

**After Optimization:**  
![CLI Test After - highest-gpa](screenshots/cli-test highest-gpa-after.jpg)

**Optimization Applied:**
- Used `ORDER BY GPA DESC LIMIT 1` for fast retrieval.
- Eliminated Java-based loop searching.
- Query now **retrieves only the top student** efficiently.

---

### **4. Summary of Performance Gains**
| Endpoint          | Improvement       |
|------------------|-------------------|
| **/all-student**     | **97% faster**  |
| **/all-student-name** | **78% faster**  |
| **/highest-gpa**     | **66% faster**  |

✅ **All endpoints achieved more than the required 20% improvement!**

</details>