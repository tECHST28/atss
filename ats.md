# ATS Lab — All 23 Practicals

## Quick Reference

| P# | Practical | Algorithm |
|---|---|---|
| 1 | Rank students — admission (top 10) | Bubble Sort |
| 2 | Shortlist internship candidates (top 10) | Selection Sort |
| 3 | Exam leaderboard (top 10) | Insertion Sort |
| 4 | Placement-eligible students | Bubble Sort (Optimized) |
| 5 | Online platform learner ranking | Selection Sort |
| 6 | Top athletes selection | Insertion Sort |
| 7 | Library books by accession number | Insertion Sort |
| 8 | GCD to simplify ratios | Euclidean Algorithm |
| 9 | Fibonacci sequence | Recursion + Iteration |
| 10 | Search element in unsorted list | Sequential Search |
| 11 | Search element in sorted array | Binary Search |
| 12 | Sort list efficiently | Merge Sort |
| 13 | Arrange by priority | Heap Sort |
| 14 | Sort dataset quickly | Quick Sort |
| 15 | Improve sorting efficiency | Randomized Quick Sort |
| 16 | Maximize profit — knapsack | Fractional Knapsack (Greedy) |
| 17 | Schedule jobs within deadlines | Job Sequencing (Greedy) |
| 18 | Minimum spanning tree | Kruskal's Algorithm |
| 19 | Minimum cost spanning tree | Prim's Algorithm |
| 20 | Shortest path from source | Dijkstra's Algorithm |
| 21 | N-Queens problem | Backtracking |
| 22 | 8-Queens problem (optimized) | Backtracking |
| 23 | 4-Queens on 4×4 board | Backtracking |

---

## Complexity Cheat Sheet

| Algorithm | Best | Average | Worst | Space | Stable |
|---|---|---|---|---|---|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Rand. Quick Sort | O(n log n) | O(n log n) | O(n log n) expected | O(log n) | No |
| Sequential Search | O(1) | O(n) | O(n) | O(1) | — |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) | — |
| GCD (Euclidean) | — | O(log min(a,b)) | — | O(1) | — |
| Kruskal's | — | O(E log E) | — | O(V) | — |
| Prim's | — | O(V²) | — | O(V) | — |
| Dijkstra's | — | O(V²) | — | O(V) | — |

---

## How to Compile and Run Java

```bash
# Compile
javac P1_BubbleSort.java

# Run
java P1_BubbleSort

# Compile and run in one line
javac P1_BubbleSort.java && java P1_BubbleSort
```

---

---

# Practical 1 — Rank Students for Admission (Top 10)

**Algorithm:** Bubble Sort | **AIM:** Sort admission scores descending, display top 10.

## Code

```java
// P1_BubbleSort.java
import java.util.Arrays;

public class P1_BubbleSort {
    static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] < arr[j + 1]) {    // descending order
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] scores = {85,92,78,95,88,76,99,84,91,87,73,96,82,89,94,79,90,83,77,93};
        bubbleSort(scores);
        System.out.println("Top 10 Admission Candidates:");
        for (int i = 0; i < 10; i++)
            System.out.println("Rank " + (i+1) + ": " + scores[i]);
    }
}
```

## Viva Q&A

**Q: What is Bubble Sort?**
> It repeatedly compares adjacent elements and swaps them if in the wrong order. After each pass, the largest unsorted element 'bubbles' to its correct position.

**Q: Time complexity of Bubble Sort?**
> O(n²) worst and average case. O(n) best case when array is already sorted (with the swapped flag optimisation).

**Q: Is Bubble Sort stable?**
> Yes. It only swaps when strictly less than (not equal), so equal elements maintain their relative order.

**Q: Space complexity?**
> O(1) — in-place. Only uses a temp variable for swapping.

**Q: How did you sort in descending order?**
> Changed the comparison from `arr[j] > arr[j+1]` (ascending) to `arr[j] < arr[j+1]` (descending).

---

# Practical 2 — Shortlist Internship Candidates (Top 10)

**Algorithm:** Selection Sort | **AIM:** Sort test scores descending, display top 10.

## Code

```java
// P2_SelectionSort.java
public class P2_SelectionSort {
    static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int maxIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] > arr[maxIdx])    // descending
                    maxIdx = j;
            }
            int temp = arr[maxIdx];
            arr[maxIdx] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] scores = {88,72,95,81,67,90,85,78,92,74,96,83,70,87,91,76,84,93,69,89};
        selectionSort(scores);
        System.out.println("Top 10 Internship Candidates:");
        for (int i = 0; i < 10; i++)
            System.out.println("Rank " + (i+1) + ": " + scores[i]);
    }
}
```

## Viva Q&A

**Q: How does Selection Sort work?**
> Finds the maximum element from the unsorted portion and swaps it with the first element of the unsorted portion. Repeats until sorted.

**Q: How many swaps does Selection Sort do?**
> Exactly O(n) swaps — one per pass. Better than Bubble Sort when writes are costly (e.g., flash memory).

**Q: Is Selection Sort stable?**
> No. It can swap a non-adjacent element, changing the relative order of equal elements.

**Q: Compare Bubble Sort vs Selection Sort.**
> Both O(n²) time, O(1) space. Bubble Sort does O(n²) swaps. Selection Sort does only O(n) swaps. Bubble Sort is stable, Selection Sort is not.

**Q: Is there a best case improvement for Selection Sort?**
> No. It always scans the full unsorted portion to find the maximum, so it's always O(n²) regardless of input order.

---

# Practical 3 — Exam Leaderboard (Top 10)

**Algorithm:** Insertion Sort | **AIM:** Sort exam scores descending to create a leaderboard.

## Code

```java
// P3_InsertionSort.java
public class P3_InsertionSort {
    static void insertionSort(int[] arr) {
        int n = arr.length;
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] < key) {    // descending
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        int[] scores = {85,92,78,95,88,76,99,84,91,87,73,96,82,89,94,79,90,83,77,93};
        insertionSort(scores);
        System.out.println("Exam Leaderboard - Top 10:");
        for (int i = 0; i < 10; i++)
            System.out.println("Rank " + (i+1) + ": " + scores[i]);
    }
}
```

## Viva Q&A

**Q: How does Insertion Sort work?**
> Builds a sorted portion one element at a time. For each new element, finds its correct position in the sorted portion by shifting larger elements right, then inserts it.

**Q: Best case for Insertion Sort?**
> O(n) when already sorted — the inner while loop never executes.

**Q: When is Insertion Sort preferred?**
> For small arrays (n < 20) and nearly-sorted arrays. Low overhead, cache-friendly, stable, in-place. Many libraries use it for small subarrays.

**Q: Is Insertion Sort stable?**
> Yes. Only shifts when strictly less than the key, so equal elements maintain relative order.

**Q: What is the analogy for Insertion Sort?**
> Like sorting a hand of playing cards — pick each new card and insert it into the correct position in your already-sorted hand.

---

# Practical 4 — Placement-Eligible Students (Bubble Sort Optimized)

**Algorithm:** Bubble Sort with swapped flag | **AIM:** Sort aptitude scores and filter above threshold.

## Code

```java
// P4_BubbleSortPlacement.java
public class P4_BubbleSortPlacement {
    static int bubbleSortOptimized(int[] arr) {
        int n = arr.length;
        int passes = 0;
        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] < arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            passes++;
            if (!swapped) break;    // already sorted — early exit
        }
        return passes;
    }

    public static void main(String[] args) {
        int[] scores = {70,85,60,90,75,88,65,92,80,55,95,72,68,83,78,91,62,87,74,66};
        int passes = bubbleSortOptimized(scores);
        System.out.println("Sorted in " + passes + " passes");
        System.out.println("Placement Eligible (score >= 75):");
        for (int s : scores)
            if (s >= 75) System.out.println("Score: " + s + " - ELIGIBLE");
    }
}
```

## Viva Q&A

**Q: What is the optimisation in Bubble Sort?**
> A `swapped` boolean flag. If no swaps happen in a pass, the array is already sorted — break early. Gives O(n) best case for already-sorted input.

**Q: How does the swapped flag work?**
> Set `swapped=false` before each pass. If any swap occurs, set it to `true`. After the pass, if still false, no elements were out of order — sorted, so break.

**Q: What is a threshold-based filter?**
> After sorting, iterate and only display elements above a cutoff (e.g., score >= 75). Sorting first makes this an efficient O(n) scan.

**Q: How many passes does worst-case Bubble Sort take?**
> n-1 passes for an array of size n. Each pass guarantees the i-th largest element reaches its correct position.

---

# Practical 5 — Online Platform Learner Ranking (Top 10)

**Algorithm:** Selection Sort with parallel arrays | **AIM:** Rank learners, keeping names aligned with scores.

## Code

```java
// P5_SelectionSortLearners.java
public class P5_SelectionSortLearners {
    static void selectionSort(int[] scores, String[] names) {
        int n = scores.length;
        for (int i = 0; i < n - 1; i++) {
            int maxIdx = i;
            for (int j = i + 1; j < n; j++)
                if (scores[j] > scores[maxIdx]) maxIdx = j;
            // swap scores AND names together
            int tempScore = scores[maxIdx]; scores[maxIdx] = scores[i]; scores[i] = tempScore;
            String tempName = names[maxIdx]; names[maxIdx] = names[i]; names[i] = tempName;
        }
    }

    public static void main(String[] args) {
        int[] scores = {88,72,95,81,67,90,85,78,92,74,96,83,70,87,91,76,84,93,69,89};
        String[] names = {"Alice","Bob","Carol","Dave","Eve","Frank","Grace","Henry",
                          "Ivy","Jack","Kim","Leo","Mia","Nick","Olivia","Paul",
                          "Quinn","Rose","Sam","Tom"};
        selectionSort(scores, names);
        System.out.println("Top 10 Learners:");
        for (int i = 0; i < 10; i++)
            System.out.println("Rank " + (i+1) + ": " + names[i] + " - " + scores[i]);
    }
}
```

## Viva Q&A

**Q: How did you keep names aligned with scores?**
> Used a parallel array for names. Every time two scores are swapped, the corresponding names are also swapped in the same step.

**Q: What is a parallel array?**
> Two arrays where index i of each stores related data for the same entity. `scores[i]` and `names[i]` both belong to the same student — must swap both together.

**Q: Why Selection Sort here?**
> Fewer swaps (O(n) vs O(n²)). When swapping paired arrays, fewer swaps = less work.

---

# Practical 6 — Select Top 10 Athletes

**Algorithm:** Insertion Sort with parallel arrays | **AIM:** Sort athlete performance scores keeping names.

## Code

```java
// P6_InsertionSortAthletes.java
public class P6_InsertionSortAthletes {
    static void insertionSort(int[] scores, String[] names) {
        int n = scores.length;
        for (int i = 1; i < n; i++) {
            int keyScore = scores[i];
            String keyName = names[i];
            int j = i - 1;
            while (j >= 0 && scores[j] < keyScore) {
                scores[j + 1] = scores[j];
                names[j + 1] = names[j];
                j--;
            }
            scores[j + 1] = keyScore;
            names[j + 1] = keyName;
        }
    }

    public static void main(String[] args) {
        int[] scores = {85,72,91,68,95,80,77,88,74,93,82,70,96,79,86,73,90,76,83,89};
        String[] names = {"Arjun","Priya","Rahul","Sneha","Vikas","Anita","Rohan","Neha",
                          "Karan","Divya","Suresh","Pooja","Amit","Riya","Sanjay",
                          "Kavya","Vikram","Nisha","Arun","Deepa"};
        insertionSort(scores, names);
        System.out.println("Top 10 Athletes:");
        for (int i = 0; i < 10; i++)
            System.out.println("Rank " + (i+1) + ": " + names[i] + " - " + scores[i]);
    }
}
```

## Viva Q&A

**Q: How does Insertion Sort with parallel arrays work?**
> Save both the key score and key name before the while loop. As we shift elements right in scores, also shift corresponding names. Then place both key values at the found position.

**Q: Advantage of Insertion Sort for nearly-sorted data?**
> Nearly-sorted means few shifts needed — best case approaches O(n). Very efficient for real-world datasets that are partially ordered.

**Q: What if two athletes have the same score?**
> Insertion Sort is stable — athletes with equal scores maintain their original relative order since we only shift when strictly less than the key.

---

# Practical 7 — Arrange Library Books by Accession Number

**Algorithm:** Insertion Sort ascending | **AIM:** Sort books by accession number in shelf order.

## Code

```java
// P7_InsertionSortLibrary.java
public class P7_InsertionSortLibrary {
    static void insertionSort(int[] acc, String[] titles) {
        int n = acc.length;
        for (int i = 1; i < n; i++) {
            int keyAcc = acc[i];
            String keyTitle = titles[i];
            int j = i - 1;
            while (j >= 0 && acc[j] > keyAcc) {    // ascending for accession numbers
                acc[j + 1] = acc[j];
                titles[j + 1] = titles[j];
                j--;
            }
            acc[j + 1] = keyAcc;
            titles[j + 1] = keyTitle;
        }
    }

    public static void main(String[] args) {
        int[] accNums = {1045,1012,1078,1003,1056,1034,1089,1023,1067,1001};
        String[] titles = {"Data Structures","Algorithms","Java Programming",
                           "Database Systems","Operating Systems","Computer Networks",
                           "Software Engineering","Discrete Math","AI Fundamentals","Compiler Design"};
        insertionSort(accNums, titles);
        System.out.println("Library Book Order:");
        for (int i = 0; i < accNums.length; i++)
            System.out.println(accNums[i] + " -> " + titles[i]);
    }
}
```

## Viva Q&A

**Q: Why ascending order here?**
> Library books are physically shelved in ascending accession number order for easy retrieval. Descending is for rankings; ascending is for catalogues.

**Q: What is an accession number?**
> A unique sequential identifier assigned to each book when it enters the library. Sorting by accession number = physical shelf order.

---

# Practical 8 — GCD to Simplify Ratios

**Algorithm:** Euclidean Algorithm (Recursion) | **AIM:** Find GCD using recursion and simplify ratios.

## Code

```java
// P8_GCD.java
public class P8_GCD {
    static int gcd(int a, int b) {
        if (b == 0) return a;           // base case
        return gcd(b, a % b);           // recursive case
    }

    static void simplifyRatio(int a, int b) {
        int g = gcd(a, b);
        System.out.println("GCD of " + a + " and " + b + " = " + g);
        System.out.println("Simplified ratio: " + (a/g) + " : " + (b/g));
    }

    public static void main(String[] args) {
        simplifyRatio(48, 18);
        simplifyRatio(100, 75);
        simplifyRatio(56, 98);
        simplifyRatio(360, 240);
        // LCM using GCD
        int x = 12, y = 18;
        int lcm = (x * y) / gcd(x, y);
        System.out.println("LCM of " + x + " and " + y + " = " + lcm);
    }
}
```

## Viva Q&A

**Q: What is GCD?**
> Greatest Common Divisor — the largest positive integer that divides both numbers without remainder. `gcd(48,18)=6`.

**Q: Explain the Euclidean algorithm.**
> Based on: `gcd(a,b) = gcd(b, a%b)`. Repeatedly replace the larger number with the remainder until remainder is 0. The last non-zero value is the GCD.

**Q: What is the base case?**
> When `b==0`, return `a`. Because `gcd(a,0)=a`.

**Q: How do you find LCM using GCD?**
> `LCM(a,b) = (a × b) / GCD(a,b)`.

**Q: Time complexity?**
> O(log(min(a,b))) — much faster than checking all divisors up to min(a,b).

---

# Practical 9 — Fibonacci Sequence

**Algorithm:** Recursion / Iteration / Memoization | **AIM:** Generate Fibonacci using all three approaches.

## Code

```java
// P9_Fibonacci.java
public class P9_Fibonacci {
    // 1. Recursive — simple but O(2^n)
    static long fibRecursive(int n) {
        if (n <= 1) return n;
        return fibRecursive(n-1) + fibRecursive(n-2);
    }

    // 2. Iterative — O(n) time, O(1) space
    static long fibIterative(int n) {
        if (n <= 1) return n;
        long a = 0, b = 1;
        for (int i = 2; i <= n; i++) {
            long c = a + b;
            a = b;
            b = c;
        }
        return b;
    }

    // 3. Memoized — O(n) time, O(n) space
    static long[] memo = new long[100];
    static long fibMemo(int n) {
        if (n <= 1) return n;
        if (memo[n] != 0) return memo[n];
        memo[n] = fibMemo(n-1) + fibMemo(n-2);
        return memo[n];
    }

    public static void main(String[] args) {
        System.out.println("Fibonacci Sequence (first 15 terms):");
        for (int i = 0; i < 15; i++) System.out.print(fibIterative(i) + " ");
        System.out.println();
        System.out.println("F(10) recursive = " + fibRecursive(10));
        System.out.println("F(10) iterative = " + fibIterative(10));
        System.out.println("F(10) memoized  = " + fibMemo(10));
    }
}
```

## Viva Q&A

**Q: What is the Fibonacci sequence?**
> Each number is the sum of the two preceding: 0,1,1,2,3,5,8,13,21... F(0)=0, F(1)=1, F(n)=F(n-1)+F(n-2).

**Q: Time complexity of recursive Fibonacci?**
> O(2^n) — exponential. Each call spawns two more. F(50) makes ~2^50 calls — very slow.

**Q: What is memoization?**
> Stores already-computed values. Before computing, check if answer is already stored. Reduces recursive Fibonacci from O(2^n) to O(n).

**Q: Time complexity of iterative Fibonacci?**
> O(n) time, O(1) space — just two variables updated in a loop. Most efficient.

**Q: Golden ratio connection?**
> Ratio F(n)/F(n-1) approaches φ ≈ 1.618 as n increases. Fibonacci appears in nature: flower petals, spiral shells, leaf arrangements.

---

# Practical 10 — Sequential Search in Unsorted List

**Algorithm:** Sequential (Linear) Search | **AIM:** Search for an element by scanning every element.

## Code

```java
// P10_SequentialSearch.java
public class P10_SequentialSearch {
    static int sequentialSearch(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++)
            if (arr[i] == target) return i;    // found
        return -1;                              // not found
    }

    static void searchAll(int[] arr, int target) {
        boolean found = false;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                System.out.println("Found " + target + " at index " + i);
                found = true;
            }
        }
        if (!found) System.out.println(target + " not found.");
    }

    public static void main(String[] args) {
        int[] data = {64,25,12,22,11,45,33,18,67,42,29,55};
        int target = 33;
        int idx = sequentialSearch(data, target);
        if (idx != -1) System.out.println("Element " + target + " found at index " + idx);
        else System.out.println("Element not found");
        searchAll(data, 22);
        searchAll(data, 100);
    }
}
```

## Viva Q&A

**Q: What is Sequential Search?**
> Scans each element one by one from the beginning until target is found or end is reached. Works on both sorted and unsorted arrays.

**Q: Time complexity?**
> O(n) worst/average case. O(1) best case (element at index 0).

**Q: When prefer Sequential over Binary Search?**
> When array is unsorted and sorting would be too costly. Also for very small arrays.

**Q: Why return -1 for not found?**
> -1 is a sentinel value meaning 'not found'. Since -1 is not a valid array index, it clearly signals absence without a separate boolean flag.

---

# Practical 11 — Binary Search in Sorted Array

**Algorithm:** Binary Search | **AIM:** Locate a target in a sorted array using both iterative and recursive approaches.

## Code

```java
// P11_BinarySearch.java
public class P11_BinarySearch {
    // Iterative
    static int binarySearch(int[] arr, int target) {
        int low = 0, high = arr.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;    // avoids integer overflow
            if (arr[mid] == target) return mid;
            else if (arr[mid] < target) low = mid + 1;
            else high = mid - 1;
        }
        return -1;
    }

    // Recursive
    static int binarySearchRecursive(int[] arr, int low, int high, int target) {
        if (low > high) return -1;
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) return binarySearchRecursive(arr, mid+1, high, target);
        else return binarySearchRecursive(arr, low, mid-1, target);
    }

    public static void main(String[] args) {
        int[] sorted = {2,5,8,12,16,23,38,45,56,72,91};
        int target = 23;
        System.out.println("Iterative: " + target + " at index " + binarySearch(sorted, target));
        System.out.println("Recursive: " + target + " at index " +
            binarySearchRecursive(sorted, 0, sorted.length-1, target));
        System.out.println("Search 100: " + binarySearch(sorted, 100));
    }
}
```

## Viva Q&A

**Q: How does Binary Search work?**
> Checks the middle element. If equal to target, done. If target is greater, search right half. If smaller, search left half. Halves the search space each step. Requires sorted array.

**Q: Why use `mid = low + (high-low)/2` instead of `(low+high)/2`?**
> Prevents integer overflow. If low and high are both close to `Integer.MAX_VALUE`, their sum overflows. The alternative gives the same result safely.

**Q: Time complexity?**
> O(log n) — each comparison eliminates half the elements. For 1 million elements, only ~20 comparisons needed.

**Q: Precondition for Binary Search?**
> Array MUST be sorted. Binary Search on an unsorted array gives incorrect results.

**Q: Sequential vs Binary Search?**
> Sequential: O(n), works on unsorted. Binary: O(log n), requires sorted. For large sorted arrays, Binary Search is vastly faster.

---

# Practical 12 — Merge Sort

**Algorithm:** Merge Sort (Divide and Conquer) | **AIM:** Sort a list efficiently using Merge Sort.

## Code

```java
// P12_MergeSort.java
public class P12_MergeSort {
    static void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1, n2 = right - mid;
        int[] L = new int[n1], R = new int[n2];
        for (int i = 0; i < n1; i++) L[i] = arr[left + i];
        for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];
        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2)
            arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];
        while (i < n1) arr[k++] = L[i++];
        while (j < n2) arr[k++] = R[j++];
    }

    static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }

    public static void main(String[] args) {
        int[] arr = {64,34,25,12,22,11,90,45,67,38};
        System.out.print("Before: "); for (int x : arr) System.out.print(x + " ");
        mergeSort(arr, 0, arr.length - 1);
        System.out.print("\nAfter:  "); for (int x : arr) System.out.print(x + " ");
    }
}
```

## Viva Q&A

**Q: What paradigm does Merge Sort use?**
> Divide and Conquer. Divides array in half recursively until single elements, then merges sorted halves back together.

**Q: Time complexity?**
> O(n log n) in all cases — best, average, worst. No O(n²) worst case unlike Quick Sort.

**Q: Space complexity?**
> O(n) — needs extra arrays L and R for merging. Not in-place. Main disadvantage vs Quick Sort.

**Q: Is Merge Sort stable?**
> Yes. In the merge step, `L[i] <= R[j]` takes from L first — equal elements maintain relative order.

**Q: When prefer Merge Sort over Quick Sort?**
> When stability is required, worst-case O(n²) is unacceptable, or for linked lists and external sorting (data larger than RAM).

---

# Practical 13 — Heap Sort

**Algorithm:** Heap Sort | **AIM:** Arrange elements by priority using Heap Sort.

## Code

```java
// P13_HeapSort.java
public class P13_HeapSort {
    static void heapify(int[] arr, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        if (left < n && arr[left] > arr[largest])   largest = left;
        if (right < n && arr[right] > arr[largest])  largest = right;
        if (largest != i) {
            int temp = arr[i]; arr[i] = arr[largest]; arr[largest] = temp;
            heapify(arr, n, largest);    // recursively heapify affected subtree
        }
    }

    static void heapSort(int[] arr) {
        int n = arr.length;
        for (int i = n/2 - 1; i >= 0; i--) heapify(arr, n, i);    // build max heap
        for (int i = n - 1; i > 0; i--) {
            int temp = arr[0]; arr[0] = arr[i]; arr[i] = temp;     // swap root to end
            heapify(arr, i, 0);    // heapify reduced heap
        }
    }

    public static void main(String[] args) {
        int[] arr = {12,11,13,5,6,7,90,45,33,22};
        System.out.print("Before: "); for (int x : arr) System.out.print(x + " ");
        heapSort(arr);
        System.out.print("\nAfter:  "); for (int x : arr) System.out.print(x + " ");
    }
}
```

## Viva Q&A

**Q: What is a Max Heap?**
> A complete binary tree where every parent is greater than or equal to its children. Root is always the maximum. Array storage: for node i, left child = 2i+1, right child = 2i+2.

**Q: Explain Heap Sort steps.**
> Step 1: Build max heap from the array. Step 2: Repeatedly swap the root (maximum) with the last element and heapify the reduced heap. Result: sorted ascending array.

**Q: Time complexity?**
> O(n log n) in all cases. Building the heap is O(n); each extraction with heapify is O(log n) for n elements.

**Q: Is Heap Sort stable?**
> No. Swapping the root with the last element can change the relative order of equal elements.

**Q: What is heapify?**
> Fixes a heap violation at a given node. Compares node with its children, swaps with the largest child if needed, then recursively heapifies the affected subtree. O(log n).

---

# Practical 14 — Quick Sort

**Algorithm:** Quick Sort | **AIM:** Sort a dataset quickly using Quick Sort.

## Code

```java
// P14_QuickSort.java
public class P14_QuickSort {
    static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];    // last element as pivot
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
            }
        }
        int temp = arr[i+1]; arr[i+1] = arr[high]; arr[high] = temp;
        return i + 1;
    }

    static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    public static void main(String[] args) {
        int[] arr = {64,34,25,12,22,11,90,45,67,38,55,29};
        System.out.print("Before: "); for (int x : arr) System.out.print(x + " ");
        quickSort(arr, 0, arr.length - 1);
        System.out.print("\nAfter:  "); for (int x : arr) System.out.print(x + " ");
    }
}
```

## Viva Q&A

**Q: How does Quick Sort work?**
> Selects a pivot, partitions array so elements <= pivot go left and > pivot go right, then recursively sorts both halves. After partition, pivot is in its final sorted position.

**Q: Worst case for Quick Sort?**
> O(n²) when pivot is always the smallest or largest element — happens with already sorted or reverse sorted arrays when using last/first element as pivot.

**Q: Average time complexity?**
> O(n log n). With a good pivot (near median), array splits roughly in half giving log n levels, each requiring O(n) partitioning work.

**Q: Is Quick Sort stable?**
> No. Partitioning can change relative order of equal elements.

**Q: Why is Quick Sort often faster than Merge Sort in practice?**
> Better cache performance (in-place), lower constant factors, no extra memory for merging.

---

# Practical 15 — Randomized Quick Sort

**Algorithm:** Randomized Quick Sort | **AIM:** Improve sorting efficiency with random pivot selection.

## Code

```java
// P15_RandomizedQuickSort.java
import java.util.Random;

public class P15_RandomizedQuickSort {
    static Random rand = new Random();

    static int randomizedPartition(int[] arr, int low, int high) {
        int pivotIdx = low + rand.nextInt(high - low + 1);    // random pivot
        int temp = arr[pivotIdx]; arr[pivotIdx] = arr[high]; arr[high] = temp;
        int pivot = arr[high];
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
            }
        }
        temp = arr[i+1]; arr[i+1] = arr[high]; arr[high] = temp;
        return i + 1;
    }

    static void randomizedQuickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = randomizedPartition(arr, low, high);
            randomizedQuickSort(arr, low, pi - 1);
            randomizedQuickSort(arr, pi + 1, high);
        }
    }

    public static void main(String[] args) {
        int[] arr = {64,34,25,12,22,11,90,45,67,38};
        System.out.print("Before: "); for (int x : arr) System.out.print(x + " ");
        randomizedQuickSort(arr, 0, arr.length - 1);
        System.out.print("\nAfter:  "); for (int x : arr) System.out.print(x + " ");
        System.out.println("\nRandomized QSort avoids O(n²) worst case!");
    }
}
```

## Viva Q&A

**Q: How does Randomized Quick Sort differ from regular Quick Sort?**
> Instead of always using the last element as pivot, it randomly selects any element from [low, high], swaps it to last position, then runs the standard partition.

**Q: Why does random pivot help?**
> O(n²) worst case only occurs for specific bad inputs (sorted arrays). With random pivot, no specific input consistently causes worst case — expected time is O(n log n) for ALL inputs.

**Q: What is `rand.nextInt(high - low + 1)`?**
> Generates a random integer from 0 to (high-low) inclusive. Adding low shifts it to range [low, high] — a uniformly random pivot index in the current subarray.

**Q: Expected time complexity?**
> Expected O(n log n) for all inputs. The probability of hitting O(n²) decreases exponentially.

---

# Practical 16 — Fractional Knapsack

**Algorithm:** Greedy | **AIM:** Maximize profit by selecting items (or fractions) within capacity.

## Code

```java
// P16_FractionalKnapsack.java
import java.util.Arrays;

public class P16_FractionalKnapsack {
    static double fractionalKnapsack(int capacity, int[] weights, int[] values) {
        int n = weights.length;
        double[][] items = new double[n][3];    // [value, weight, ratio]
        for (int i = 0; i < n; i++) {
            items[i][0] = values[i];
            items[i][1] = weights[i];
            items[i][2] = (double) values[i] / weights[i];    // value per unit weight
        }
        Arrays.sort(items, (a, b) -> Double.compare(b[2], a[2]));    // sort by ratio desc
        double totalValue = 0;
        int remaining = capacity;
        for (double[] item : items) {
            if (remaining <= 0) break;
            if (item[1] <= remaining) {
                totalValue += item[0];
                remaining -= item[1];
                System.out.printf("Take full item: value=%.0f weight=%.0f%n", item[0], item[1]);
            } else {
                double fraction = remaining / item[1];
                totalValue += fraction * item[0];
                System.out.printf("Take %.2f fraction: value=%.2f%n", fraction, fraction * item[0]);
                remaining = 0;
            }
        }
        return totalValue;
    }

    public static void main(String[] args) {
        int[] weights = {2,3,5,7,1,4,6};
        int[] values  = {10,15,20,25,8,18,24};
        int capacity  = 15;
        double maxProfit = fractionalKnapsack(capacity, weights, values);
        System.out.printf("Maximum Profit = %.2f%n", maxProfit);
    }
}
```

## Viva Q&A

**Q: What is the Fractional Knapsack problem?**
> Given items with weights and values and a knapsack of capacity W, select items (or fractions) to maximize total value. Fractions are allowed — unlike 0/1 Knapsack.

**Q: What is the greedy strategy?**
> Sort items by value-to-weight ratio descending. Take full items first; when capacity runs out, take as much fraction as possible of the next item.

**Q: Why greedy works for Fractional but not 0/1 Knapsack?**
> In Fractional, taking partial amounts is allowed so highest-ratio item is always optimal. In 0/1, we must take or leave the whole item — greedy can miss better combinations, requiring dynamic programming.

**Q: Time complexity?**
> O(n log n) due to sorting. Greedy selection itself is O(n).

**Q: What is value-to-weight ratio?**
> Value gained per unit weight used. Prioritizing high ratio ensures maximum value for space consumed.

---

# Practical 17 — Job Sequencing

**Algorithm:** Greedy | **AIM:** Schedule jobs to maximize profit within deadlines.

## Code

```java
// P17_JobSequencing.java
import java.util.Arrays;

public class P17_JobSequencing {
    public static void main(String[] args) {
        char[] jobs     = {'J1','J2','J3','J4','J5'};
        int[]  deadlines = {2, 1, 2, 1, 3};
        int[]  profits   = {100, 19, 27, 25, 15};
        int n = jobs.length;

        // Sort by profit descending
        Integer[] idx = new Integer[n];
        for (int i = 0; i < n; i++) idx[i] = i;
        Arrays.sort(idx, (a, b) -> profits[b] - profits[a]);

        int maxDeadline = Arrays.stream(deadlines).max().getAsInt();
        char[]   schedule = new char[maxDeadline + 1];
        boolean[] slot    = new boolean[maxDeadline + 1];
        int totalProfit = 0;

        for (int i : idx) {
            for (int j = deadlines[i]; j >= 1; j--) {    // find latest free slot
                if (!slot[j]) {
                    slot[j] = true;
                    schedule[j] = jobs[i];
                    totalProfit += profits[i];
                    break;
                }
            }
        }

        System.out.print("Job Schedule: ");
        for (int j = 1; j <= maxDeadline; j++)
            if (slot[j]) System.out.print(schedule[j] + " ");
        System.out.println("\nTotal Profit: " + totalProfit);
    }
}
```

## Viva Q&A

**Q: What is the Job Sequencing problem?**
> Given n jobs with deadlines and profits, schedule at most one job per time unit so jobs complete by their deadline, maximizing total profit.

**Q: Greedy strategy?**
> Sort jobs by profit descending. For each job, assign it to the latest available slot <= its deadline.

**Q: Why latest slot instead of earliest?**
> Using the latest slot keeps earlier slots free for future jobs with tighter deadlines — maximises chance of fitting all high-profit jobs.

**Q: Time complexity?**
> O(n²) — for each of n jobs, scan up to n slots. Can be O(n log n) with Union-Find.

---

# Practical 18 — Kruskal's MST

**Algorithm:** Kruskal's + Union-Find | **AIM:** Construct minimum spanning tree.

## Code

```java
// P18_Kruskal.java
import java.util.Arrays;

public class P18_Kruskal {
    static int[] parent, rank;

    static int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]);    // path compression
        return parent[x];
    }

    static void union(int x, int y) {
        int px = find(x), py = find(y);
        if (rank[px] < rank[py]) parent[px] = py;
        else if (rank[px] > rank[py]) parent[py] = px;
        else { parent[py] = px; rank[px]++; }
    }

    public static void main(String[] args) {
        int V = 4;
        int[][] edges = {{0,1,10},{0,2,6},{0,3,5},{1,3,15},{2,3,4}};
        Arrays.sort(edges, (a, b) -> a[2] - b[2]);    // sort by weight
        parent = new int[V]; rank = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        System.out.println("Kruskal's MST edges:");
        int mstWeight = 0;
        for (int[] edge : edges) {
            int u = edge[0], v = edge[1], w = edge[2];
            if (find(u) != find(v)) {    // no cycle
                union(u, v);
                System.out.println("Edge (" + u + "-" + v + ") weight=" + w);
                mstWeight += w;
            }
        }
        System.out.println("MST Total Weight: " + mstWeight);
    }
}
```

## Viva Q&A

**Q: What is a Minimum Spanning Tree (MST)?**
> A spanning tree with minimum total edge weight. Connects all V vertices using exactly V-1 edges with no cycles.

**Q: How does Kruskal's work?**
> Sort all edges by weight. Add edges one by one using Union-Find — if two endpoints are in different components (no cycle), add the edge. Stop when V-1 edges are added.

**Q: What is Union-Find?**
> Tracks which vertices are in the same connected component. `find(x)` returns the root of x's component. `union(x,y)` merges two components. Detects cycles.

**Q: What is path compression?**
> When calling `find(x)`, all nodes on path to root are directly connected to root. Flattens the tree making future `find()` calls nearly O(1) amortized.

**Q: Kruskal's vs Prim's?**
> Kruskal's: edge-based, sorts all edges, better for sparse graphs. Prim's: vertex-based, grows from a vertex, better for dense graphs. Both produce the same MST.

---

# Practical 19 — Prim's MST

**Algorithm:** Prim's Algorithm | **AIM:** Build minimum cost spanning tree starting from a vertex.

## Code

```java
// P19_Prim.java
public class P19_Prim {
    static final int INF = Integer.MAX_VALUE;

    static void primMST(int[][] graph, int V) {
        int[] key    = new int[V];      // min edge weight to include vertex
        int[] parent = new int[V];      // MST parent
        boolean[] inMST = new boolean[V];
        for (int i = 0; i < V; i++) { key[i] = INF; parent[i] = -1; }
        key[0] = 0;    // start from vertex 0

        for (int count = 0; count < V - 1; count++) {
            // Pick min key vertex not in MST
            int u = -1;
            for (int v = 0; v < V; v++)
                if (!inMST[v] && (u == -1 || key[v] < key[u])) u = v;
            inMST[u] = true;
            // Update neighbours
            for (int v = 0; v < V; v++)
                if (graph[u][v] != 0 && !inMST[v] && graph[u][v] < key[v]) {
                    key[v] = graph[u][v];
                    parent[v] = u;
                }
        }

        System.out.println("Prim's MST edges:");
        int total = 0;
        for (int i = 1; i < V; i++) {
            System.out.println("Edge (" + parent[i] + "-" + i + ") weight=" + key[i]);
            total += key[i];
        }
        System.out.println("MST Total Weight: " + total);
    }

    public static void main(String[] args) {
        int[][] graph = {
            {0,2,0,6,0}, {2,0,3,8,5}, {0,3,0,0,7}, {6,8,0,0,9}, {0,5,7,9,0}
        };
        primMST(graph, 5);
    }
}
```

## Viva Q&A

**Q: How does Prim's work?**
> Starts from any vertex. At each step, adds the minimum weight edge connecting an MST vertex to a non-MST vertex. Repeats until all vertices are included.

**Q: What is the key[] array?**
> `key[v]` stores the minimum edge weight needed to include vertex v into the MST from the current MST set. Initially infinity for all except source (key[0]=0).

**Q: Time complexity?**
> O(V²) with adjacency matrix. O(E log V) with min-priority queue — better for sparse graphs.

**Q: Prim's vs Kruskal's graph representation?**
> Kruskal uses edge list. Prim uses adjacency matrix or list. Kruskal sorts edges globally; Prim grows locally from a vertex.

---

# Practical 20 — Dijkstra's Shortest Path

**Algorithm:** Dijkstra's Algorithm | **AIM:** Find shortest path from source to all vertices.

## Code

```java
// P20_Dijkstra.java
public class P20_Dijkstra {
    static final int INF = Integer.MAX_VALUE;

    static void dijkstra(int[][] graph, int src, int V) {
        int[]     dist    = new int[V];
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++) dist[i] = INF;
        dist[src] = 0;

        for (int count = 0; count < V - 1; count++) {
            // Pick unvisited vertex with minimum distance
            int u = -1;
            for (int v = 0; v < V; v++)
                if (!visited[v] && (u == -1 || dist[v] < dist[u])) u = v;
            visited[u] = true;
            // Relax neighbours
            for (int v = 0; v < V; v++)
                if (!visited[v] && graph[u][v] != 0 && dist[u] != INF
                    && dist[u] + graph[u][v] < dist[v])
                    dist[v] = dist[u] + graph[u][v];
        }

        System.out.println("Shortest distances from source " + src + ":");
        for (int i = 0; i < V; i++)
            System.out.println("To vertex " + i + ": " + (dist[i] == INF ? "INF" : dist[i]));
    }

    public static void main(String[] args) {
        int[][] graph = {
            {0,4,0,0,0,0,0,8,0}, {4,0,8,0,0,0,0,11,0}, {0,8,0,7,0,4,0,0,2},
            {0,0,7,0,9,14,0,0,0}, {0,0,0,9,0,10,0,0,0}, {0,0,4,14,10,0,2,0,0},
            {0,0,0,0,0,2,0,1,6}, {8,11,0,0,0,0,1,0,7}, {0,0,2,0,0,0,6,7,0}
        };
        dijkstra(graph, 0, 9);
    }
}
```

## Viva Q&A

**Q: How does Dijkstra's work?**
> Starts at source (dist=0). Picks the unvisited vertex with minimum distance, marks it visited, then relaxes distances to its neighbours. Greedy — never revisits a vertex.

**Q: What is edge relaxation?**
> If `dist[u] + weight(u,v) < dist[v]`, update `dist[v]`. A shorter path to v was found through u.

**Q: Time complexity?**
> O(V²) with adjacency matrix. O((V+E) log V) with min-priority queue — better for sparse graphs.

**Q: Dijkstra's limitation?**
> Does NOT work with negative edge weights. Use Bellman-Ford for negative weights.

**Q: Dijkstra vs Prim's — how are they similar?**
> Both use the same greedy structure — pick minimum distance/key unvisited vertex, update neighbours. Dijkstra finds shortest paths from source; Prim's finds MST. Update condition differs.

---

# Practical 21 — N-Queens Problem

**Algorithm:** Backtracking | **AIM:** Place N queens on N×N board — no two attack each other.

## Code

```java
// P21_NQueens.java
public class P21_NQueens {
    static int N;
    static int[] board;    // board[i] = column of queen in row i
    static int solutions = 0;

    static boolean isSafe(int row, int col) {
        for (int r = 0; r < row; r++) {
            if (board[r] == col) return false;                           // same column
            if (Math.abs(board[r] - col) == Math.abs(r - row)) return false;  // diagonal
        }
        return true;
    }

    static void solve(int row) {
        if (row == N) {
            solutions++;
            System.out.print("Solution " + solutions + ": ");
            for (int i = 0; i < N; i++) System.out.print("(" + i + "," + board[i] + ") ");
            System.out.println();
            return;
        }
        for (int col = 0; col < N; col++) {
            if (isSafe(row, col)) {
                board[row] = col;
                solve(row + 1);
                board[row] = -1;    // backtrack
            }
        }
    }

    public static void main(String[] args) {
        N = 8;    // change to any N
        board = new int[N];
        java.util.Arrays.fill(board, -1);
        solve(0);
        System.out.println("Total solutions for " + N + "-Queens: " + solutions);
    }
}
```

## Viva Q&A

**Q: What is the N-Queens problem?**
> Place N queens on an N×N chessboard such that no two queens share the same row, column, or diagonal.

**Q: What is Backtracking?**
> A systematic algorithm that tries all possibilities. When a partial solution violates constraints, it 'backtracks' to the previous decision point and tries a different choice. Prunes the search space.

**Q: How does isSafe() work?**
> For each previously placed queen in rows 0 to row-1, check: (1) same column: `board[r]==col`. (2) same diagonal: `|row-r| == |col-board[r]|`. If either true, unsafe.

**Q: Time complexity?**
> O(N!) worst case. But pruning via isSafe() eliminates most branches early, making it much faster in practice.

**Q: How many solutions does 8-Queens have?**
> 92 distinct solutions. N=4: 2, N=5: 10, N=6: 4, N=7: 40, N=8: 92.

---

# Practical 22 — 8-Queens Problem (Optimized)

**Algorithm:** Backtracking with board printing | **AIM:** Place 8 queens, show first 3 solutions visually.

## Code

```java
// P22_EightQueens.java
public class P22_EightQueens {
    static int[] queens = new int[8];
    static int count = 0;

    static boolean isSafe(int row, int col) {
        for (int r = 0; r < row; r++) {
            if (queens[r] == col) return false;
            if (Math.abs(queens[r] - col) == Math.abs(r - row)) return false;
        }
        return true;
    }

    static void solve(int row) {
        if (row == 8) {
            count++;
            if (count <= 3) {    // show first 3 solutions
                System.out.println("Solution " + count + ":");
                printBoard();
            }
            return;
        }
        for (int col = 0; col < 8; col++) {
            if (isSafe(row, col)) {
                queens[row] = col;
                solve(row + 1);
            }
        }
    }

    static void printBoard() {
        for (int r = 0; r < 8; r++) {
            for (int c = 0; c < 8; c++)
                System.out.print(queens[r] == c ? "Q " : ". ");
            System.out.println();
        }
        System.out.println();
    }

    public static void main(String[] args) {
        solve(0);
        System.out.println("Total solutions: " + count);    // 92
    }
}
```

## Viva Q&A

**Q: How is 8-Queens different from N-Queens?**
> 8-Queens is a specific instance with N=8 and exactly 92 solutions. The algorithm is identical — 8-Queens is the classic example because it's large enough to be interesting but small enough to visualize.

**Q: What does the board look like?**
> Q = queen, . = empty. Each row has exactly one Q, and no two Qs share a column or diagonal.

**Q: What optimisations can be applied?**
> Bitmask optimisation: track used columns and diagonals using integer bits for O(1) conflict check. Symmetry: solve only first 4 columns of row 0 and mirror for other 4 solutions.

---

# Practical 23 — 4-Queens on 4×4 Board

**Algorithm:** Backtracking | **AIM:** Place 4 queens on 4×4 board — show all 2 solutions with visual board.

## Code

```java
// P23_FourQueens.java
public class P23_FourQueens {
    static int[] queens = new int[4];
    static int count = 0;

    static boolean isSafe(int row, int col) {
        for (int r = 0; r < row; r++) {
            if (queens[r] == col) return false;
            if (Math.abs(queens[r] - col) == Math.abs(r - row)) return false;
        }
        return true;
    }

    static void solve(int row) {
        if (row == 4) {
            count++;
            System.out.println("Solution " + count + ":");
            printBoard();
            return;
        }
        for (int col = 0; col < 4; col++) {
            if (isSafe(row, col)) {
                queens[row] = col;
                solve(row + 1);
                queens[row] = 0;    // explicit backtrack
            }
        }
    }

    static void printBoard() {
        System.out.println("  0 1 2 3");
        for (int r = 0; r < 4; r++) {
            System.out.print(r + " ");
            for (int c = 0; c < 4; c++)
                System.out.print(queens[r] == c ? "Q " : ". ");
            System.out.println();
        }
        System.out.println();
    }

    public static void main(String[] args) {
        solve(0);
        System.out.println("Total solutions for 4-Queens: " + count);    // 2
    }
}
```

## Viva Q&A

**Q: How many solutions does 4-Queens have?**
> Exactly 2 solutions. Solution 1: queens at columns (1,3,0,2). Solution 2: (2,0,3,1) — the mirror image.

**Q: Trace backtracking for 4-Queens, row 0 col 0.**
> Place (0,0). Try (1,0): same column — fail. (1,1): diagonal — fail. (1,2): safe, place. Try (2,0): same col as row 0 — fail. (2,1): diagonal — fail. (2,2): same col — fail. (2,3): diagonal — fail. Backtrack to row 1, try col 3...

**Q: What does backtracking mean physically?**
> When no safe column exists for current row, remove the queen we placed in the previous row (`queens[row]=0`) and try the next column in that row. We 'undo' a choice and try the next option.

**Q: Why is 4-Queens a good exam example?**
> Small enough to trace by hand (4×4). Exactly 2 solutions — verifiable manually. Shows the complete backtracking process: explore, prune, backtrack, explore again.

---

## Common Viva Questions Across All Practicals

**Q: What is the difference between Divide and Conquer and Greedy?**
> Divide and Conquer (Merge Sort, Quick Sort) breaks the problem into subproblems, solves them recursively, combines results. Greedy (Knapsack, Job Sequencing) makes the locally optimal choice at each step without reconsidering — simpler but doesn't always give the globally optimal solution.

**Q: What is the difference between Greedy and Dynamic Programming?**
> Greedy makes one locally optimal choice per step (fast but may miss global optimum). Dynamic Programming solves all subproblems and stores results (always optimal but uses more memory). Fractional Knapsack = Greedy. 0/1 Knapsack = DP.

**Q: What is in-place sorting?**
> A sort that requires O(1) extra space — only rearranges elements within the original array. Bubble, Selection, Insertion, Heap, Quick Sort are all in-place. Merge Sort is NOT in-place (requires O(n) extra space).

**Q: What is a stable sort?**
> A sort that preserves the relative order of equal elements. Bubble, Insertion, Merge Sort are stable. Selection, Heap, Quick Sort are NOT stable.

**Q: What is Backtracking?**
> An algorithmic technique that builds a solution incrementally and abandons (backtracks) a partial solution as soon as it determines that it cannot lead to a valid complete solution. Used in N-Queens, Sudoku, maze solving.
