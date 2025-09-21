# Button Mash

## 📖 Problem Description
You are given a device with a display and three buttons: `+1`, `-1`, and `×2`. The display starts at `0`.

Calculate the **minimum number of button presses** required to display an integer `n`.

### Rules
- The device cannot display negative numbers.
- Pressing `-1` when the display is `0` will cause a malfunction.

### Example
To reach the number `59`, the minimum sequence of button presses is:
```
+1, +1, ×2, ×2, ×2, -1, ×2, ×2, -1
```
This requires **9 operations**.

---

## 🔢 Input
- Line 1: An integer `n`.

## 🔢 Output
- Line 1: The minimum number of button presses to display `n`.

## ⚙️ Constraints
- `1 ≤ n ≤ 10^6`

## 📝 Example
### Input
```
59
```
### Output
```
9
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

        if(n == 0)
        {
            Console.WriteLine(0);
            return;
        }

        int count = 0;

        while (n > 1)
        {
            if (n % 2 == 0)
            {
                n /= 2;
                count++;
            }
            else
            {
                if ((n + 1) % 4 == 0)
                {
                    n++;
                }
                else
                {
                    n--;
                }
                count++;
            }

            if (n == 1)
            {
                count++;
            }
        }

        Console.WriteLine(count);
    }
}
```