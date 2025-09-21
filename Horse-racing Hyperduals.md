# Horse-racing Hyperduals

## 📖 Problem Description
Casablanca’s hippodrome is organizing **hyperduals**: races with only two horses where the goal is to select horses with **similar strengths**.

A horse's strength is represented by a bidimensional vector `(Velocity, Elegance)`. The **distance** between two strengths `(V1,E1)` and `(V2,E2)` is:
```
abs(V2-V1) + abs(E2-E1)
```

Write a program to identify the **two closest strengths** and output their distance.

---

## 🔢 Input
- Line 1: An integer `N` representing the number of horses.
- Next `N` lines: two integers `Vi` and `Ei` separated by space, representing each horse's velocity and elegance.

## 🔢 Output
- Line 1: The distance `D` between the two closest strengths.

## ⚙️ Constraints
- `10 ≤ N ≤ 600`
- `0 ≤ Vi,Ei ≤ 10000000`
- `D ≥ 0`
- All values are integers.

## 📝 Example
### Input
```
10
6850207 0
8707138 0
8028585 0
3635318 0
8612162 0
6854699 0
7106093 0
3721952 0
2670046 0
1746583 0
```
### Output
```
4492
```

---

## 💻 C# Solution
```csharp
using System;

class Solution
{
    static void Main()
    {
        int N = int.Parse(Console.ReadLine());
        int[,] horses = new int[N, 2];

        for (int i = 0; i < N; i++)
        {
            string[] parts = Console.ReadLine().Split();
            horses[i, 0] = int.Parse(parts[0]);
            horses[i, 1] = int.Parse(parts[1]);
        }

        int minDist = int.MaxValue;

        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                int v1 = horses[i, 0], e1 = horses[i, 1];
                int v2 = horses[j, 0], e2 = horses[j, 1];
                int d = Math.Abs(v1 - v2) + Math.Abs(e1 - e2);
                if (d < minDist) minDist = d;
            }
        }

        Console.WriteLine(minDist);
    }
}
```