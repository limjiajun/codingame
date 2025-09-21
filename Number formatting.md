# Number Formatting

## 📖 Problem Description
Based on a specially formatted number `numberstring`, output the number divided by two in the **same special format**.

### Special Format Rules:
- The number is represented as a string of **length 19**.
- It represents a float with **9 numbers before** and **6 numbers after** the decimal point.
- Numbers before the decimal are **comma-separated every 3 digits**.
- Numbers after the decimal are **point-separated every 3 digits**.
- Unused positions are represented by `x`.

Example:
- Input: `xxx,x38,858.321.82x`
- Actual number: `38858.32182`
- Divided by 2: `19429.16091`
- Output: `xxx,x19,429.160.91x`

---

## 🔢 Input
- Line 1: A string `numberstring` of length 19 representing a number in the special format.

## 🔢 Output
- A string of length 19 representing the number divided by 2 in the same special format.

## ⚙️ Constraints
- `numberstring` represents a number >= 0 and <= 999999999.999998
- The last character of `numberstring` is always either `x` or an even number.

## 📝 Example
### Input
```
200,000,000.000.002
```
### Output
```
100,000,000.000.001
```

---

## 💻 C# Solution
```csharp
using System;

class Solution
{
    static void Main(string[] args)
    {
        string input = Console.ReadLine(); // e.g., "200,000,000.000.002"
        char[] chars = input.ToCharArray();
        int carry = 0;

        for (int i = 0; i < chars.Length; i++)
        {
            char c = chars[i];
            if (c >= '0' && c <= '9')
            {
                int num = (c - '0') + carry * 10;
                chars[i] = (char)('0' + num / 2);
                carry = num % 2;
            }
        }

        string result = new string(chars);
        Console.WriteLine(result);
    }
}
```