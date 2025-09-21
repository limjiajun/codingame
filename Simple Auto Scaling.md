# Simple Auto-Scaling

## 📖 Problem Description
Implement a **simple auto-scaling system** for services across a datacenter.

- Each service can handle a maximum number of clients per instance.
- You will receive metrics representing the number of clients connected to each service.
- Output the number of instances to start or stop for each metric line.
- Positive value → start instances
- Negative value → stop instances
- Instances are rounded up: `ceil(clients / capacity)`.
- Initially, no instances are running.

Reference: [Auto-scaling Wikipedia](https://en.wikipedia.org/wiki/Autoscaling)

---

## 🔢 Input
1. Line 1: `S M` → number of services and number of metric lines.
2. Line 2: `S` integers → capacity of each service (clients per instance).
3. Next `M` lines: `S` integers each → number of clients connected for each service.

## 🔢 Output
- `M` lines: number of instances to **start/stop** for each metric line.
- For the first line, output the number of required instances.
- For subsequent lines, output the difference from the previous line.

## ⚙️ Constraints
- `0 < S ≤ 50`
- `0 < M ≤ 100`
- Services can handle at least 1 client.

## 📝 Example
### Input
```
4 3
5 10 4 3
20 5 10 7
25 3 14 16
15 4 20 10
```
### Output
```
4 1 3 3
1 0 1 3
-2 0 1 -2
```

---

## 💻 C# Solution
```csharp
using System;

class Solution
{
    static void Main(string[] args)
    {
        string[] inputs = Console.ReadLine().Split(' ');
        int S = int.Parse(inputs[0]);
        int M = int.Parse(inputs[1]);

        inputs = Console.ReadLine().Split(' ');
        int[] capacities = new int[S];
        for (int i = 0; i < S; i++) capacities[i] = int.Parse(inputs[i]);

        int[][] allInstances = new int[M][];
        for (int i = 0; i < M; i++)
        {
            inputs = Console.ReadLine().Split(' ');
            int[] instances = new int[S];
            for (int j = 0; j < S; j++)
                instances[j] = (int)Math.Ceiling((double)int.Parse(inputs[j]) / capacities[j]);
            allInstances[i] = instances;
        }

        for (int i = 0; i < M; i++)
        {
            for (int j = 0; j < S; j++)
            {
                if (j > 0) Console.Write(" ");
                Console.Write(i == 0 ? allInstances[i][j] : allInstances[i][j] - allInstances[i - 1][j]);
            }
            Console.WriteLine();
        }
    }
}
```

