# QA Theory: Week 2

## 1. Equivalence Partitioning:

* Equivalence Partitioning (EP) is a test design technique that divides all possible data into groups (classes), assuming that the program processes the elements within a single group in exactly the same way.  

*The main principle behind this method* is that if one test with a value from a given group detects a defect, then any other value from that same group will detect the exact same defect. This eliminates the need to test all possible values; to verify the system, it is sufficient to select just one value from each class.  

*Classes can be defined for any type of data.* Groups can be continuous or discrete, finite or infinite, but they must not intersect with one another and cannot be empty sets.  

*Valid partitions:* Contain valid values that the program must accept and process according to the specification.  
*Invalid partitions:* Contain invalid values that the program must reject, ignore, or for which no processing logic is specified in the requirements.  

*Working with Multiple Parameters (Each Choice Coverage):* We often test objects with multiple input parameters (for example, a form with login and password fields), which means there are several sets of classes involved. The simplest criterion for such cases is called “Each Choice coverage.” It requires that test cases cover every class from each set at least once, but it does not force the tester to verify absolutely every combination of these classes with one another.

---

## 2. Boundary Value Analysis: 

* Boundary Value Analysis (BVA) is a testing technique that stems directly from Equivalence Partitioning (EP) and is based on testing the boundaries of these classes. The main rationale behind this method is that developers most often make mistakes precisely at the boundaries of ranges.

*Key rule:* BVA can only be applied to ordered data (where there are clear minimum and maximum values that can be arranged in order). If any two elements belong to the same class, then all values between them must also belong to that class.

1. *The 2-value BVA Approach (Two-Value Verification):* In this approach, for each boundary, both the boundary value itself and its nearest neighbor—which belongs to the adjacent (opposite) class—are tested. To achieve 100% coverage using this method, test cases must cover all identified boundary values.   

 2. *3-value BVA Approach (Three-Value Verification):* Here, for each boundary, the boundary itself and both of its neighbors—both outside and inside the class—are tested. This means that some of the values being tested will not be boundaries at all.  To achieve 100% coverage, all of these boundaries and all of their neighbors must be tested.   
 
 *Why is the 3-value approach better than the 2-value approach?*
The 3-value approach is more rigorous and helps identify defects that the 2-value method simply won’t detect.

---

## 3. Tables: password length 8–20 characters, quantity of 1 to 10, discount percentage from 0 to 100. 2-value and 3-value checks on the password table.

*Table 1: password*
| Class | Range | Value |
| --- | --- | --- |
| Invalid (<) | <8 | 7 |
| Valid | 8-20 | 9 |
| Invalid (>) | >20 | 25 |
| Invalid | empty | 0 |  

*BVA 2-value: 7, 8; 20, 21;*  
*BVA 3-value: 7, 8, 9;  19, 20, 21;*

---

*Table 2: quantity*
| Class | Range | Value |
| --- | --- | --- |
| Invalid (<) | <1 | 0 |
| Valid | 1-10 | 3 |
| Invalid (>) | >10 | 12 |
| Invalid (not a number) | letters, symbols | "abc" |
| Invalid | empty | 0 |  
| Invalid | non-integer | 2.5 | 
  
---

*Table 3: discount percentage*
| Class | Range | Value |
| --- | --- | --- |
| Invalid (<) | <0 | -2 |
| Valid | 0-100 | 6 |
| Invalid (>) | >100 | 105 |
| Invalid (not a number) | letters, symbols | "abc" |
| Invalid | empty | 0 |  
| Invalid | non-integer | 2.5 | 

---
