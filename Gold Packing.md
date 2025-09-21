# Gold Packing

## 📖 Problem Description
You are packing `n` gold bars of uniform height and width but variable length into a box of length `m` with the same height and width. Your task is to find the **set of gold bars** that uses up the **most space** in the box.

- If multiple sets use the same space, choose the one with the **fewest number of bars**.
- If still multiple sets exist, choose the one that is **lexicographically smallest** (minimize the first bar, then the second, etc.).

---

## 🔢 Input
1. Line 1: Integer `m` (length of the box).
2. Line 2: Integer `n` (number of gold bars).
3. Line 3: `n` space-separated integers representing the lengths of the gold bars, sorted from shortest to longest.

## 🔢 Output
- The lengths of gold bars separated by space, sorted from shortest to longest.

## ⚙️ Constraints
- `0 < m <= 2000`
- `0 < n <= 20`

## 📝 Example
### Input
```
7
5
5 6 7 8 9
```
### Output
```
7
```

---

## 💻 C# Solution
```csharp
using System;
using System.Collections.Generic;

class Solution
{
    static void Main()
    {
        int m = int.Parse(Console.ReadLine());
        int n = int.Parse(Console.ReadLine());
        string[] parts = Console.ReadLine().Split();
        int[] bars = new int[n];
        for (int i = 0; i < n; i++)
            bars[i] = int.Parse(parts[i]);

        List<int> bestSolution = new List<int>();
        int bestSum = 0;

        int total = 1 << n; // 2^n combinations
        for (int mask = 0; mask < total; mask++)
        {
            List<int> current = new List<int>();
            int sum = 0;

            for (int i = 0; i < n; i++)
            {
                if ((mask & (1 << i)) != 0)
                {
                    current.Add(bars[i]);
                    sum += bars[i];
                }
            }

            if (sum > m) continue;

            if (sum > bestSum ||
                (sum == bestSum && current.Count < bestSolution.Count) ||
                (sum == bestSum && current.Count == bestSolution.Count && IsLexSmaller(current, bestSolution)))
            {
                bestSolution = new List<int>(current);
                bestSum = sum;
            }
        }

        bestSolution.Sort();
        Console.WriteLine(string.Join(" ", bestSolution));
    }

    static bool IsLexSmaller(List<int> a, List<int> b)
    {
        a.Sort();
        b.Sort();
        for (int i = 0; i < a.Count; i++)
        {
            if (a[i] < b[i]) return true;
            if (a[i] > b[i]) return false;
        }
        return false;
    }
}
```