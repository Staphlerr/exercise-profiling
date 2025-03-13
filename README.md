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
![CLI Test Before - all-student](screenshots/cli-test%20all-student.jpg)

**After Optimization:**  
![CLI Test After - all-student](screenshots/cli-test%20all-student-after.jpg)

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
![CLI Test Before - all-student-name](screenshots/cli-test%20all-student-name.jpg)

**After Optimization:**  
![CLI Test After - all-student-name](screenshots/cli-test%20all-student-name-after.jpg)

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
![CLI Test Before - highest-gpa](screenshots/cli-test%20highest-gpa.jpg)

**After Optimization:**  
![CLI Test After - highest-gpa](screenshots/cli-test%20highest-gpa-after.jpg)

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

<details>
<summary><b>Reflection for Module 5</b></summary>

## 3. Reflection on Performance Testing and Profiling

### 1. What is the difference between the approach of performance testing with JMeter and profiling with IntelliJ Profiler in the context of optimizing application performance?
JMeter is used to **simulate real-world user traffic and measure response times**, helping us evaluate how well the system performs under load. It provides quantitative results such as response times, throughput, and latency.

On the other hand, IntelliJ Profiler is used to **analyze the internal workings of the application** at a more granular level. It allows us to identify bottlenecks in the code, such as inefficient loops, slow database queries, and memory-intensive operations. While JMeter helps us see the impact of optimizations, IntelliJ Profiler helps us find what needs to be optimized.

### 2. How does the profiling process help you in identifying and understanding the weak points in your application?
Profiling provides detailed insights into CPU usage, method execution times, and memory consumption. Using the **Flame Graph** and **Method List Tab**, we were able to:
- Identify the N+1 Query Problem, which was causing multiple redundant database calls.
- Find that string concatenation in loops was slowing down the `/all-student-name` endpoint.
- Observe that sorting in Java for the highest GPA was inefficient compared to sorting directly in the database.

These insights guided us in applying optimizations that significantly improved response times.

### 3. Do you think IntelliJ Profiler is effective in assisting you to analyze and identify bottlenecks in your application code?
Yes, IntelliJ Profiler is extremely effective because it provides a **visual representation of performance hotspots**. Instead of guessing which part of the code is slow, we can directly see the most expensive methods in terms of execution time. The comparison feature also helped us verify improvements after optimization.

### 4. What are the main challenges you face when conducting performance testing and profiling, and how do you overcome these challenges?
**Challenges:**
1. **Inconsistent performance measurements** – The first run is always slower due to JVM Just-In-Time (JIT) compilation.
2. **Understanding flame graphs** – Initially, interpreting the profiler output was complex.
3. **Database caching effects** – PostgreSQL caching sometimes caused inconsistent query execution times.

**Solutions:**
1. **Repeated measurements** – We ignored the first run and took an average of multiple executions.
2. **Learning the profiler tools** – We explored different tabs (Method List, Flame Graph) to break down performance issues.
3. **Flushing database cache** – Restarting PostgreSQL ensured we got realistic query execution times.

### 5. What are the main benefits you gain from using IntelliJ Profiler for profiling your application code?
- Pinpoints exact slow methods rather than relying on guesswork.
- Helps compare before-and-after results to see actual performance improvements.
- Identifies CPU vs. Total Execution Time, allowing better optimizations.
- Provides real-time insights into database queries and method execution.

### 6. How do you handle situations where the results from profiling with IntelliJ Profiler are not entirely consistent with findings from performance testing using JMeter?
Sometimes, JMeter results do not align perfectly with IntelliJ Profiler findings due to factors like network latency, database cache effects, and garbage collection cycles. To handle this:
- We analyze multiple profiling sessions to ensure consistency.
- We clear database caches between runs to get accurate SQL execution times.
- We compare CPU time instead of total execution time in the profiler to eliminate system noise.
- If discrepancies still exist, we test each method individually using unit tests to isolate the bottlenecks.

### 7. What strategies do you implement in optimizing application code after analyzing results from performance testing and profiling? How do you ensure the changes you make do not affect the application's functionality?
**Optimization Strategies:**
1. **Fixing the N+1 query issue** → Used `JOIN FETCH` to fetch related data in one query.
2. **Replacing Java-based sorting with SQL queries** → Used `ORDER BY GPA DESC LIMIT 1`.
3. **Avoiding inefficient string concatenation** → Used `Collectors.joining()` instead of `+` in a loop.

**Ensuring Functionality Remains Intact:**
- **Regression Testing**: Verified the API responses remained unchanged.
- **Comparing Database Queries**: Ensured the optimized queries returned the same results as the old implementation.

---
### Conclusion
By combining JMeter for load testing and IntelliJ Profiler for deep code analysis, this program has succeeded to **optimize all three endpoints by over 60%** while ensuring no loss of functionality. The key takeaway is that **profiling and performance testing must be done together to achieve the best improvements**.

</details>
