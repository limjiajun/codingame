# Leaking Bathtub Problem

## Problem Description

Bob wants to fill his bathtub with water, but there are some leaks that let water escape.  

The bathtub is a rectangular parallelepiped with:  
- Surface area `S` (cm²)  
- Height `h` (cm)  

Water flows from the tap at `flow` L/min.  
Each leak is defined by:  
- `leakHeight` (cm): the water height at which the leak starts  
- `leakFlow` (L/min): water lost through that leak  

**Goal:** Calculate the time, rounded **down to the nearest second**, required to fill the bathtub.  
If the bathtub cannot be filled completely due to leaks, output `"Impossible"` along with the maximum filled height.

---

### Input

- Line 1: Integer `S`, surface area (cm²)  
- Line 2: Integer `h`, bathtub height (cm)  
- Line 3: Integer `flow`, tap water flow (L/min)  
- Line 4: Integer `N`, number of leaks  
- Next `N` lines: Two space-separated integers `leakHeight` and `leakFlow`

---

### Output

- If bathtub can be filled:  
  Time in `HH:MM:SS` format, rounded down to the second
- If bathtub cannot be filled:  
  `Impossible, filling_height cm`

---

### Constraints

- `0 ≤ N ≤ 1000`  
- `0 ≤ leakHeight < h`  
- `0 < time ≤ 99:59:59`  
- `0 < S*h < 2^32`

---

## Example

### Input

    12750
    60
    12
    2
    20 1
    45 3

### Output

    01:14:08

---

## Explanation

1. **Tap flow**: 12 L/min  
2. **Leak 1**: starts at 20 cm, 1 L/min  
3. **Leak 2**: starts at 45 cm, 3 L/min  

**Simulation by height (cm):**  
- 0–19: netFlow = 12 → water rises  
- 20–44: netFlow = 12 − 1 = 11 → water rises  
- 45–59: netFlow = 12 − 1 − 3 = 8 → water rises  

**Total time:** 01:14:08

---

## C# Solution

```csharp
using System;

class Solution
{
    static void Main(string[] args)
    {
        int S = int.Parse(Console.ReadLine());    // Bathtub surface area (cm²)
        int h = int.Parse(Console.ReadLine());    // Bathtub height (cm)
        int flow = int.Parse(Console.ReadLine()); // Tap flow (L/min)
        int n = int.Parse(Console.ReadLine());    // Number of leaks

        int[] leakHeight = new int[n];
        int[] leakFlow = new int[n];
        for (int i = 0; i < n; i++)
        {
            string[] inputs = Console.ReadLine().Split(' ');
            leakHeight[i] = int.Parse(inputs[0]);
            leakFlow[i] = int.Parse(inputs[1]);
        }

        double totalSeconds = 0;
        int currentHeight = 0;

        while (currentHeight < h)
        {
            int netFlow = flow;

            for (int i = 0; i < n; i++)
                if (leakHeight[i] <= currentHeight)
                    netFlow -= leakFlow[i];

            if (netFlow <= 0)
            {
                Console.WriteLine($"Impossible, {currentHeight} cm.");
                return;
            }

            double volume = S / 1000.0; // liters for 1 cm height
            totalSeconds += volume / netFlow * 60.0; // seconds to fill 1 cm
            currentHeight++;
        }

        long sec = (long)totalSeconds;
        Console.WriteLine($"{sec/3600:00}:{(sec%3600)/60:00}:{sec%60:00}");
    }
}
```

