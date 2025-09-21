# Metric Unit Conversion Problem

## 📖 Problem Description

You are given an expression of the form `valueunit + valueunit`.\
The goal is to **add the two values** after converting them to the
**smaller unit** among the two.

Example: `4cm + 2dm`

-   Convert `2dm` to `cm`: `2dm = 20cm`\
-   Add values: `4cm + 20cm = 24cm`

------------------------------------------------------------------------

## 🔢 Input

-   Line 1: A string representing the expression to calculate,
    e.g. `1m + 1cm`

------------------------------------------------------------------------

## 🔢 Output

-   A string of the form `valueunit`\
-   The `value` is the sum after conversion to the smaller unit\
-   The `unit` is the smaller unit of the two given values

------------------------------------------------------------------------

## ⚙️ Constraints

-   `0 <= value <= 1000` (real number with precision ≤ 0.00001)\
-   Unit can be one of: `um`, `mm`, `cm`, `dm`, `m`, `km`

Conversion rules:\
- 1 mm = 1000 um\
- 1 cm = 10 mm\
- 1 dm = 10 cm\
- 1 m = 10 dm\
- 1 km = 1000 m

------------------------------------------------------------------------

## 📝 Example

### Input

    1m + 1cm

### Output

    101cm

------------------------------------------------------------------------

## 💻 C# Solution

``` csharp
using System;
using System.Collections.Generic;

class Solution
{
    static void Main()
    {
        string expression = Console.ReadLine(); // e.g. "4cm + 2dm"
        string[] parts = expression.Split('+');

        // Conversion factors: unit → micrometers
        var factor = new Dictionary<string, double>
        {
            { "um", 1 },
            { "mm", 1000 },
            { "cm", 10000 },
            { "dm", 100000 },
            { "m",  1000000 },
            { "km", 1000000000 }
        };

        // Function to parse "value+unit" into (value, unit)
        (double val, string unit) Parse(string s)
        {
            s = s.Trim();
            foreach (var u in factor.Keys)
            {
                if (s.EndsWith(u))
                {
                    double v = double.Parse(s.Substring(0, s.Length - u.Length));
                    return (v, u);
                }
            }
            throw new Exception("Invalid unit");
        }

        var (v1, u1) = Parse(parts[0]);
        var (v2, u2) = Parse(parts[1]);

        // Convert both to micrometers
        double totalUm = v1 * factor[u1] + v2 * factor[u2];

        // Determine smaller unit (the one with smaller factor)
        string finalUnit = factor[u1] < factor[u2] ? u1 : u2;

        // Convert back into that unit
        double finalValue = totalUm / factor[finalUnit];

        Console.WriteLine($"{finalValue}{finalUnit}");
    }
}
```
