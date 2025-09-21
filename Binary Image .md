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
        // Step 1: Read the number of rows (height of the graphic)
        int n = int.Parse(Console.ReadLine()); 

        // Step 2: Prepare a list to store the decoded rows
        List<string> rows = new List<string>();

        // Step 3: Variable to store the length of the first row
        // This ensures all rows have the same length
        int rowLength = -1;

        // Step 4: Loop over each row input
        for (int i = 0; i < n; i++)
        {
            // Step 4a: Read the encoded numbers for this row and split by space
            string[] parts = Console.ReadLine().Split(' ');

            // Step 4b: Variable to build the decoded row
            string row = "";

            // Step 4c: Start with '.' as the first color (white)
            char current = '.';

            // Step 4d: Loop through each number in the row
            foreach (string part in parts)
            {
                int count = int.Parse(part); // Convert string to integer

                // Repeat the current color 'count' times
                for (int j = 0; j < count; j++)
                    row += current;

                // Switch color for the next segment
                current = (current == '.') ? 'O' : '.';
            }

            // Step 4e: Check if all rows have the same length
            if (rowLength == -1)
                rowLength = row.Length; // First row sets the reference length
            else if (row.Length != rowLength)
            {
                Console.WriteLine("INVALID");
                return; // Exit program if inconsistent length
            }

            // Step 4f: Add the decoded row to the list
            rows.Add(row);
        }

        // Step 5: Print all decoded rows
        foreach (string r in rows)
            Console.WriteLine(r);
    }
}
```

## ✅ How It Works
1. Read the number of rows and encoded lines.
2. Decode each line by expanding the counts into `.` and `O` pixels.
3. Ensure all rows have the same length to maintain a rectangle.
4. Output decoded graphic or `INVALID` if row lengths differ.

This solution ensures a correct rectangular RLE-decoded graphic representation.