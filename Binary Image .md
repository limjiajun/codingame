# Binary Image Decoder

## 📖 Problem Description

You are going to write a simple program to decode arrays of data into a black-and-white graphic. The graphic consists of `n` lines of black and white pixels.

- `.` represents a white pixel.
- `O` represents a black pixel.

### Encoding Example

A line `....OOO.` would be encoded as `4 3 1` (4 whites, 3 blacks, 1 white). Lines starting with black include a `0` at the beginning to indicate no white pixels before the first black pixel. Example: `OO.OOOOO` → `0 2 1 5`.

**Requirement:** Output `INVALID` if the graphic is not rectangular (i.e., all decoded lines must have the same length).

## 🔢 Input

- Line 1: Integer `n` — number of rows in the graphic.
- Next `n` lines: Array of integers representing the encoded nth line.

**Constraints:**
- `n < 200`

## 🔢 Output

- If the grid is not rectangular: `INVALID`
- Otherwise: `n` lines of the decoded graphic (pixels `.` or `O`, no spaces).

## 📝 Example

**Input:**
```
4
1 3 2 1
1 3 2 1
1 3 2 1
1 3 2 1
```

**Output:**
```
.OOO..O
.OOO..O
.OOO..O
.OOO..O
```

## 💻 C# Solution

```csharp
using System;
using System.Collections.Generic;

class Solution
{
    static void Main(string[] args)
    {
        // Step 1: Read the number of rows
        int n = int.Parse(Console.ReadLine());

        // Step 2: List to store decoded rows
        var rows = new List<string>();

        // Step 3: Track length of first row to check rectangle
        int? rowLength = null;

        // Step 4: Loop through each encoded line
        for (int i = 0; i < n; i++)
        {
            string[] parts = Console.ReadLine().Split(' ');
            string row = "";

            // Step 4a: Decode the line by repeating '.' and 'O'
            for (int j = 0; j < parts.Length; j++)
            {
                int count = int.Parse(parts[j]);
                char ch = (j % 2 == 0) ? '.' : 'O';
                row += new string(ch, count);
            }

            // Step 4b: Check all rows are same length
            if (rowLength == null)
            {
                rowLength = row.Length;
            }
            else if (row.Length != rowLength)
            {
                Console.WriteLine("INVALID");
                return;
            }

            // Step 4c: Add decoded row to list
            rows.Add(row);
        }

        // Step 5: Print all rows
        foreach (var r in rows)
        {
            Console.WriteLine(r);
        }
    }
}
```

## ✅ How It Works
1. Read the number of rows and encoded lines.
2. Decode each line by expanding the counts into `.` and `O` pixels.
3. Ensure all rows have the same length to maintain a rectangle.
4. Output decoded graphic or `INVALID` if row lengths differ.

This solution ensures a correct rectangular RLE-decoded graphic representation.