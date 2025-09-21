# Snail Run


## 📖 Problem Description
You have a snail race and need to determine the winner!

- `numberSnails`: Number of snails.
- `speedSnail`: Speed of each snail.
- `mapHeight` and `mapWidth`: Dimensions of the map.

### Map Symbols
- `number` (1 to numberSnails): Snail identifier
- `*`: Walkable path
- `#`: Finish line

Snails move in 4 directions (up, down, left, right), cannot move diagonally, and choose the shortest path.

For each race, there is only one winner.

---

## 🔢 Input
1. Line 1: Integer `numberSnails`.
2. Next `numberSnails` lines: Integer `speedSnail` for each snail.
3. Next line: Integer `mapHeight`.
4. Next line: Integer `mapWidth`.
5. Next `mapHeight` lines: String representing each row of the map.

## 🔢 Output
- A single number representing the winner snail.

## ⚙️ Constraints
- `2 ≤ numberSnails ≤ 6`
- `0 ≤ speedSnail ≤ 6`
- `2 ≤ mapHeight ≤ 6`
- `5 ≤ mapWidth ≤ 9`

## 📝 Example
### Input
```
3
2
3
5
3
6
1****#
2****#
3****#
```
### Output
```
3
```

---

## 💻 C# Solution
```csharp
using System;

class Solution
{
    static void Main(string[] args)
    {
        int n = int.Parse(Console.ReadLine());
        int[] sp = new int[n], x = new int[n], y = new int[n];
        for (int i = 0; i < n; i++)
            sp[i] = int.Parse(Console.ReadLine());

        int h = int.Parse(Console.ReadLine());
        int w = int.Parse(Console.ReadLine());

        int[,] ex = new int[50, 2];
        int ec = 0;

        for (int i = 0; i < h; i++)
        {
            string row = Console.ReadLine();
            for (int j = 0; j < w; j++)
            {
                char c = row[j];
                if (c == '#')
                {
                    ex[ec, 0] = i;
                    ex[ec, 1] = j;
                    ec++;
                }
                else if (c != '*')
                {
                    int id = c - '0' - 1;
                    x[id] = i;
                    y[id] = j;
                }
            }
        }

        int winner = -1, best = 999;
        for (int i = 0; i < n; i++)
        {
            if (sp[i] == 0) continue;
            for (int e = 0; e < ec; e++)
            {
                int dist = Math.Abs(x[i] - ex[e, 0]) + Math.Abs(y[i] - ex[e, 1]);
                int time = (dist + sp[i] - 1) / sp[i];
                if (time < best)
                {
                    best = time;
                    winner = i + 1;
                }
            }
        }

        Console.WriteLine(winner);
    }
}
```

