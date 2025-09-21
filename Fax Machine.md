### Project Description: Fax Machine Decompression

An old compressed black and white fax transmission needs to be decompressed.

- The first number is the width of the decompressed image.
- The second number is the height of the decompressed image.
- The starting color is black.
- The third and remaining numbers are the number of pixels to draw from left to right, then top to bottom of the current color. After that number of pixels is filled, the color swaps.

The encoding is similar to Modified Huffman Coding used in early digital fax machines.

Example input:
```
8
3
10 10 4
```
produces output:
```
|********|
|**      |
|    ****|
```

### Input
- Line 1: Width of the image (integer)
- Line 2: Height of the image (integer)
- Line 3: Space-separated integers representing the compressed fax data

### Output
- Height lines: rows with fax output of '*' (black) and ' ' (white), each surrounded by '|'

### Constraints
- 1 ≤ Width ≤ 100
- 1 ≤ Height ≤ 100

### Example
**Input:**
```
8
3
10 10 4
```
**Output:**
```
|********|
|**      |
|    ****|
```

### C# Solution
```csharp
using System;
using System.Linq;
using System.IO;
using System.Text;
using System.Collections;
using System.Collections.Generic;

class Solution
{
     static void Main(string[] args)
    {
        int W = int.Parse(Console.ReadLine()); // read width
        int H = int.Parse(Console.ReadLine()); // read height
        string[] parts = Console.ReadLine().Split(' ');
        
        int[] runs = Array.ConvertAll(parts, int.Parse);

        char[] pixels = new char[W * H];
        bool black = true;
        int idx = 0;

        foreach (int run in runs)
        {
            for (int i = 0; i < run && idx < pixels.Length; i++)
                pixels[idx++] = black ? '*' : ' ';
            black = !black;
        }

        for (int r = 0; r < H; r++)
        {
            Console.Write("|");
            for (int c = 0; c < W; c++)
                Console.Write(pixels[r * W + c]);
            Console.WriteLine("|");
        }
    }
}
```

