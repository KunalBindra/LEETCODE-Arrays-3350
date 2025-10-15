# LEETCODE-Arrays-3350
We’re given:

```java
nums = [2, 5, 7, 8, 9, 2, 3, 4, 3, 1]
```

---

### 🧩 Step 1: Initial setup

| Variable    | Value | Meaning                               |
| ----------- | ----- | ------------------------------------- |
| `currRun`   | 1     | length of the current increasing run  |
| `prevRun`   | 0     | length of the previous increasing run |
| `maxResult` | 0     | maximum result found so far           |

---

### 🧩 Step 2: Loop starts (`i = 1` to `n-1`)

We compare each element with the previous one.

---

#### 🔸 **i = 1** → compare `5` and `2`

* `5 > 2` → still increasing
  → `currRun = 2`

Then update:

```java
maxResult = max(maxResult, currRun / 2) = max(0, 1) = 1
maxResult = max(maxResult, min(prevRun, currRun)) = max(1, min(0, 2)) = 1
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 1 | 5       | 2       | 0       | 1         |

---

#### 🔸 **i = 2** → compare `7` and `5`

* `7 > 5` → still increasing
  → `currRun = 3`

Updates:

```java
maxResult = max(1, 3/2=1) = 1
maxResult = max(1, min(0,3)=0) = 1
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 2 | 7       | 3       | 0       | 1         |

---

#### 🔸 **i = 3** → compare `8` and `7`

* `8 > 7` → still increasing
  → `currRun = 4`

Updates:

```java
maxResult = max(1, 4/2=2) = 2
maxResult = max(2, min(0,4)=0) = 2
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 3 | 8       | 4       | 0       | 2         |

---

#### 🔸 **i = 4** → compare `9` and `8`

* `9 > 8` → still increasing
  → `currRun = 5`

Updates:

```java
maxResult = max(2, 5/2=2) = 2
maxResult = max(2, min(0,5)=0) = 2
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 4 | 9       | 5       | 0       | 2         |

---

#### 🔸 **i = 5** → compare `2` and `9`

* `2 < 9` → increasing order **breaks**

So:

```java
prevRun = currRun = 5
currRun = 1
```

Now:

```java
maxResult = max(2, 1/2=0) = 2
maxResult = max(2, min(5,1)=1) = 2
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 5 | 2       | 1       | 5       | 2         |

---

#### 🔸 **i = 6** → compare `3` and `2`

* `3 > 2` → increasing
  → `currRun = 2`

Updates:

```java
maxResult = max(2, 2/2=1) = 2
maxResult = max(2, min(5,2)=2) = 2
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 6 | 3       | 2       | 5       | 2         |

---

#### 🔸 **i = 7** → compare `4` and `3`

* `4 > 3` → still increasing
  → `currRun = 3`

Updates:

```java
maxResult = max(2, 3/2=1) = 2
maxResult = max(2, min(5,3)=3) = 3 ✅
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 7 | 4       | 3       | 5       | 3         |

---

#### 🔸 **i = 8** → compare `3` and `4`

* `3 < 4` → increasing order breaks
  → `prevRun = 3`, `currRun = 1`

Then:

```java
maxResult = max(3, 1/2=0) = 3
maxResult = max(3, min(3,1)=1) = 3
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 8 | 3       | 1       | 3       | 3         |

---

#### 🔸 **i = 9** → compare `1` and `3`

* `1 < 3` → break again
  → `prevRun = 1`, `currRun = 1`

Updates:

```java
maxResult = max(3, 1/2=0) = 3
maxResult = max(3, min(1,1)=1) = 3
```

| i | nums[i] | currRun | prevRun | maxResult |
| - | ------- | ------- | ------- | --------- |
| 9 | 1       | 1       | 1       | 3         |

---

### 🧩 Step 3: Loop ends → return result

```java
return maxResult; // = 3
```

---

### ✅ Final Explanation (in plain English)

The code finds **the largest size of a balanced pair of increasing subarrays** next to each other.

Here’s what happens conceptually:

* `[2,5,7,8,9]` → increasing run of length 5
* `[2,3,4]` → next increasing run of length 3

Balanced portion between these two = `min(5, 3) = 3`

So, `maxResult = 3` ✅

---
