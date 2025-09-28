# Largest Number Problem

## Problem Description

Given an input number, output the **largest number possible** following these rules:

1. The output number must be **divisible by `D`**.
2. The output number must be created by **removing 0, 1, or 2 digits** from the input number (the **order of digits cannot be changed**).
3. If it is **not possible** to make a number following the above rules, output `0`.

---

### Input

- Line 1: A number as a string  
- Line 2: Integer `D`, the divisor

---

### Output

- Line 1: The **largest number** that meets the rules

---

### Constraints

- `1000 ≤ number ≤ 1000000000`  
- `2 ≤ D ≤ 10`

---

## Example

### Input

    3141
    3

### Output

    3141

### Input

    314159
    3

### Output

    31419

---

### Explanation

1. For `3141` divisible by `3`:  
   - Original number is divisible → output `3141`.

2. For `314159` divisible by `3`:  
   - By removing the 5th digit (`5`) → `31419` is divisible by 3 and is the **largest possible**.

---

## C# Solution

```csharp
using System;

class Solution
{
    static void Main(string[] args)
    {
        string input = Console.ReadLine();   // Original number as string
        int D = int.Parse(Console.ReadLine()); // Divisor
        long maxNumber = 0; // To store the largest divisible number
        int n = input.Length;

        // Try removing 0 digits
        long num = long.Parse(input);
        if (num % D == 0)
            maxNumber = num;

        // Try removing 1 digit
        for (int i = 0; i < n; i++)
        {
            string candidate = "";
            for (int j = 0; j < n; j++)
            {
                if (j != i)
                    candidate += input[j];
            }

            num = long.Parse(candidate);
            if (num % D == 0 && num > maxNumber)
                maxNumber = num;
        }

        // Try removing 2 digits
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                string candidate = "";
                for (int k = 0; k < n; k++)
                {
                    if (k != i && k != j)
                        candidate += input[k];
                }

                num = long.Parse(candidate);
                if (num % D == 0 && num > maxNumber)
                    maxNumber = num;
            }
        }

        // Output the largest number or 0 if none
        Console.WriteLine(maxNumber);
    }
}
```

