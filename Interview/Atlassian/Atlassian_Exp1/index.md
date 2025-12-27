# 💼 Interview Experience – Atlassian Software Engineering Role

**Type:** On-Campus Opportunity  
**Company:** Atlassian  
**Total Rounds:** 3 (Online Assessment + Technical Coding + Managerial/HR)

---

## 🧪 Round 1 – Online Assessment (OA)

The first round was an **Online Assessment** consisting of **two problem-solving questions**, focused on efficiency, correctness, and handling large inputs.

---

### 1️⃣ Product Suggestions System

**Description:**  
Designed an **autocomplete-like system** to provide product suggestions as a user types a search query.  
For every character typed, the system returned **up to three product names** that start with the current prefix, **lexicographically sorted**, and updated dynamically with each new character.

**Key Requirements:**
- Return **at most three suggestions** for each prefix  
- Suggestions must be **lexicographically sorted**  
- Efficient handling for **large product lists**

**Topics Covered:**  
Strings · Sorting · Prefix Matching · Binary Search · Trie (optional)

Reference:
- https://leetcode.com/problems/search-suggestions-system/
- https://www.geeksforgeeks.org/trie-insert-and-search/

---

### 2️⃣ Horizontal Pod Autoscaler Optimization

**Description:**  
Simulated the behavior of a **Horizontal Pod Autoscaler (HPA)** across multiple microservices.  
Each service had a number of running pods, and multiple scaling events were applied.

**Types of Events:**
- **Targeted Update:** Update pod count of a specific service  
- **Bulk Update:** Increase pod counts for all services below a given threshold  

The main challenge was to apply these updates **efficiently without iterating over the entire array repeatedly**.

**Key Requirements:**
- Efficient single-service updates  
- Optimized handling of threshold-based bulk updates  
- Output final pod counts after all events

**Topics Covered:**  
Arrays · Simulation · Optimization · Efficient Updates · Range Updates

Reference:
- https://www.geeksforgeeks.org/range-update-and-point-query/
- https://leetcode.com/problems/range-addition/

---

✅ **Outcome:** Cleared Round 1

---

## 💻 Round 2 – Technical Coding Interview

**Duration:** ~45 minutes

### 🔍 Introduction
This round focused on **algorithmic thinking, data structures, and clean coding practices**.  
The interviewer emphasized writing **readable, modular, and maintainable code**, rather than just solving the problem.

---

### 🧩 Coding Question – Longest String Chain (Variant)

**Problem Statement:**  
Given a list of words, a word **A** can connect to word **B** if adding **exactly one character** anywhere in **A** results in **B**.  
The task was to find the **length of the longest possible word chain**.

**Key Requirements:**
- Use **dynamic programming** or **hash-based memoization**
- Process words in **increasing order of length**
- Ensure **clean, class-based design**
- Separate logic from input/output

**Suggested Approach:**
- Sort words by length
- Use a map to store the longest chain ending at each word
- For each word, remove one character at every position and check previous chain length

**Topics Covered:**  
Strings · Dynamic Programming · Hashing · Greedy Optimization · Class-Based Design

Reference:
- https://leetcode.com/problems/longest-string-chain/
- https://www.geeksforgeeks.org/longest-string-chain/

---

✅ **Outcome:** Cleared Round 2

---

## 👨‍💼 Round 3 – Managerial / HR Interview

### 🔍 Introduction
This round assessed **behavioral skills, leadership potential, and cultural fit**.  
The discussion was conversational but deep.

---

### 🗂️ Key Discussion Areas
- **Resume Deep Dive:** Education, internships, experiences  
- **Projects:** Role, contributions, challenges, and impact  
- **Positions of Responsibility (PORs):** Leadership and teamwork  
- **Behavioral Questions:**  
  - Conflict resolution  
  - Decision-making  
  - Handling failures  
  - Collaboration and teamwork  

### 💡 Tips for HR Rounds
- Know your resume **thoroughly**
- Be clear about **your individual contributions**
- Prepare examples for leadership and conflict scenarios
- Maintain confidence and honesty

**Topics Covered:**  
Resume Discussion · Leadership · Teamwork · Behavioral Questions · Communication Skills

---

❌ **Outcome:** Rejected

---

## 🌟 Overall Experience

Overall, it was a **good and learning-oriented experience**.  
Since this was my **first interview**, I fumbled at a few places and felt slightly underconfident due to a lack of mock interview practice.  
However, it was a **valuable and encouraging start** to my interview journey.

---

## 💡 Advice for Others

- **Be fully prepared with your resume:**  
  Every project, POR, and experience can be questioned.
- **Practice HR questions in advance:**  
  Especially conflict resolution, leadership, strengths, and failures.
- **Focus on communication skills:**  
  Along with technical preparation, clarity and confidence matter a lot.

---

## 🏁 Final Verdict

❌ **Rejected**

---

**🗒️ Shared by:** Anonymous  

---

## 🔗 Reference Links
- https://www.atlassian.com/company/careers
- https://leetcode.com/problems/search-suggestions-system/
- https://leetcode.com/problems/longest-string-chain/
- https://www.geeksforgeeks.org/trie-insert-and-search/
- https://www.geeksforgeeks.org/longest-string-chain/
- https://www.geeksforgeeks.org/range-update-and-point-query/
- https://leetcode.com/problems/range-addition/
