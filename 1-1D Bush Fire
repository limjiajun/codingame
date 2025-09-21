# Fire Extinguishing Problem

## Problem Description

You are given multiple test cases.\
Each test case is a strip of cells, where:\
- `'f'` represents a cell **on fire**\
- `'.'` represents a cell **without fire**

A **single drop of water** can put out fire in **up to 3 consecutive
cells** starting from the cell where it lands.

### Input

-   Line 1: `N`, the number of test cases\
-   Next `N` lines: each line is a string representing the strip's fire
    status

### Output

-   Print `N` lines: each containing the **minimum number of water
    drops** required for that test case.

### Constraints

-   `1 ≤ N ≤ 100`\
-   `1 ≤ length of each line ≤ 255`

------------------------------------------------------------------------

## Example

### Input

    2
    ....f....f..
    .......fff

### Output

    2
    1

------------------------------------------------------------------------

## Explanation

1.  In `....f....f..`:
    -   First fire at index 4 → needs **1 drop** (covers 4--6)\
    -   Second fire at index 9 → needs **another drop**\
    -   Total = **2 drops**
2.  In `.......fff`:
    -   Fires are continuous (`fff`) → **1 drop** covers all three.\
    -   Total = **1 drop**

------------------------------------------------------------------------

## C# Solution

``` csharp
using System;
using System.Collections.Generic;

class Solution
{
    static void Main(string[] args)
    {
        int N = int.Parse(Console.ReadLine()); // Number of test cases
        for (int t = 0; t < N; t++)
        {
            string line = Console.ReadLine(); // Fire strip input
            int water = 0;                    // Water drop counter
            int i = 0;                        // Current index

            while (i < line.Length)
            {
                if (line[i] == 'f')           // Found fire
                {
                    water++;                  // Use one drop
                    i += 3;                   // Drop covers 3 consecutive cells
                }
                else
                {
                    i++;                      // Move to next cell
                }
            }

            Console.WriteLine(water);         // Print result for this test case
        }
    }
}
```
