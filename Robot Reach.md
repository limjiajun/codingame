# Robot Reachable Cells Problem

## 📖 Problem Description

A robot starts at the **top-left corner (0,0)** of a grid with `R` rows
and `C` columns.\
The robot can move **up, down, left, or right** to adjacent cells, but
it has a restriction:

👉 The sum of the digits of the row index plus the sum of the digits of
the column index must not exceed a given threshold `T`.

You need to count **how many cells the robot can reach**.

------------------------------------------------------------------------

## 🔢 Input

-   Line 1: Integer `R` -- number of rows in the grid\
-   Line 2: Integer `C` -- number of columns in the grid\
-   Line 3: Integer `T` -- threshold for digit sums

------------------------------------------------------------------------

## 🔢 Output

-   Line 1: The number of reachable cells.

------------------------------------------------------------------------

## ⚙️ Constraints

-   `1 <= R <= 100`\
-   `1 <= C <= 100`\
-   `0 <= T <= 100`

------------------------------------------------------------------------

## 📝 Example

### Input

    3
    3
    1

### Output

    3

------------------------------------------------------------------------

## 💡 Explanation

Grid (3×3, threshold T=1):

    (0,0) ✅  sum=0+0=0 ≤ 1
    (0,1) ✅  sum=0+1=1 ≤ 1
    (1,0) ✅  sum=1+0=1 ≤ 1
    (1,1) ❌  sum=1+1=2 > 1
    ...

So, the robot can only reach **3 cells**.

------------------------------------------------------------------------

## 💻 C# Solution

``` csharp
using System;
using System.Collections.Generic;

class Solution
{
    // Helper function: sum of digits of a number
    static int Sum(int n)
    {
        int s = 0;
        while (n > 0)
        {
            s += n % 10;
            n /= 10;
        }
        return s;
    }

    static void Main()
    {
        int R = int.Parse(Console.ReadLine());
        int C = int.Parse(Console.ReadLine());
        int T = int.Parse(Console.ReadLine());

        bool[,] visited = new bool[R, C];
        Queue<(int, int)> q = new Queue<(int, int)>();

        // Start at (0,0)
        q.Enqueue((0, 0));
        visited[0, 0] = true;

        int result = 0;

        while (q.Count > 0)
        {
            var (r, c) = q.Dequeue();
            result++;

            // Directions: down, up, right, left
            int[] dr = { 1, -1, 0, 0 };
            int[] dc = { 0, 0, 1, -1 };

            for (int i = 0; i < 4; i++)
            {
                int nr = r + dr[i];
                int nc = c + dc[i];

                // Check boundaries
                if (nr < 0 || nr >= R || nc < 0 || nc >= C) continue;

                // Already visited
                if (visited[nr, nc]) continue;

                // Threshold check
                if (Sum(nr) + Sum(nc) > T) continue;

                visited[nr, nc] = true;
                q.Enqueue((nr, nc));
            }
        }

        Console.WriteLine(result);
    }
}
```
