# NATO-Alphabet's Odd Uncles

## 📖 Problem Description
The NATO alphabet is used to spell words via phonetic representations of each letter.  
However, there have been multiple historical versions of these alphabets.

Your task is:

- **Upgrade** the input word to the **next version**, or  
- If the input is already in the **newest version**, **degrade it to the oldest version**.

---

## 🔢 Versions
### Year 1908
Authority, Bills, Capture, Destroy, Englishmen, Fractious, Galloping, High,
Invariably, Juggling, Knights, Loose, Managing, Never, Owners, Play, Queen,
Remarks, Support, The, Unless, Vindictive, When, Xpeditiously, Your, Zigzag

### Year 1917
Apples, Butter, Charlie, Duff, Edward, Freddy, George, Harry, Ink, Johnnie,
King, London, Monkey, Nuts, Orange, Pudding, Queenie, Robert, Sugar, Tommy,
Uncle, Vinegar, Willie, Xerxes, Yellow, Zebra

### Year 1927
Amsterdam, Baltimore, Casablanca, Denmark, Edison, Florida, Gallipoli, Havana,
Italia, Jerusalem, Kilogramme, Liverpool, Madagascar, New-York, Oslo, Paris,
Quebec, Roma, Santiago, Tripoli, Uppsala, Valencia, Washington, Xanthippe,
Yokohama, Zurich

### Year 1956 (NATO Standard)
Alfa, Bravo, Charlie, Delta, Echo, Foxtrot, Golf, Hotel, India, Juliett, Kilo,
Lima, Mike, November, Oscar, Papa, Quebec, Romeo, Sierra, Tango, Uniform,
Victor, Whiskey, X-ray, Yankee, Zulu

---

## 🔢 Input
- Line 1: A word spelled using an alphabet (space-separated phonetic words).

---

## 🔢 Output
- Line 1: The same word spelled out using the **next alphabet version** (or oldest if already newest).

---

## 📝 Example
### Input
Authority Bills Capture

### Output
Apples Butter Charlie

---

## 💻 C# Solution
```csharp
using System;
using System.Linq;
using System.Collections.Generic;

class Solution
{
    static void Main(string[] args)
    {
        string input = Console.ReadLine();
        string[] words = input.Split(' ');

        string[] alpha1908 = { 
            "Authority", "Bills", "Capture", "Destroy", "Englishmen", "Fractious", "Galloping", "High",
            "Invariably", "Juggling", "Knights", "Loose", "Managing", "Never", "Owners", "Play", "Queen", 
            "Remarks", "Support", "The", "Unless", "Vindictive", "When", "Xpeditiously", "Your", "Zigzag"
        };
        string[] alpha1917 = { 
            "Apples", "Butter", "Charlie", "Duff", "Edward", "Freddy", "George", "Harry", "Ink", "Johnnie",
            "King", "London", "Monkey", "Nuts", "Orange", "Pudding", "Queenie", "Robert", "Sugar", "Tommy", 
            "Uncle", "Vinegar", "Willie", "Xerxes", "Yellow", "Zebra"
        };
        string[] alpha1927 = { 
            "Amsterdam", "Baltimore", "Casablanca", "Denmark", "Edison", "Florida", "Gallipoli", "Havana", 
            "Italia", "Jerusalem", "Kilogramme", "Liverpool", "Madagascar","New-York", "Oslo", "Paris", 
            "Quebec", "Roma", "Santiago", "Tripoli", "Uppsala", "Valencia",
            "Washington", "Xanthippe", "Yokohama", "Zurich"
        };
        string[] alpha1956 = { 
            "Alfa", "Bravo", "Charlie", "Delta", "Echo", "Foxtrot", "Golf", "Hotel", "India", "Juliett", "Kilo",
            "Lima", "Mike", "November", "Oscar", "Papa", "Quebec", "Romeo", "Sierra", "Tango", "Uniform", "Victor",
            "Whiskey", "X-ray", "Yankee", "Zulu" 
        };

        List<string[]> versions = new List<string[]> { alpha1908, alpha1917, alpha1927, alpha1956 };

        int currentVersion = -1;
        for (int i = 0; i < versions.Count; i++)
        {
            if (words.All(w => versions[i].Contains(w)))
            {
                currentVersion = i;
                break;
            }
        }

        int targetVersion = (currentVersion == versions.Count - 1) ? 0 : currentVersion + 1;

        string[] result = words.Select(w =>
        {
            int index = versions[currentVersion].ToList().IndexOf(w);
            return versions[targetVersion][index];
        }).ToArray();

        Console.WriteLine(string.Join(' ', result));
    }
}
```