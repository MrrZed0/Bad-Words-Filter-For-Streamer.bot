# 🛡️ Streamer.bot Bad Word Filter (C#)

A simple **C# script for Streamer.bot** that filters bad words from user input and replaces them with `*`.

Perfect for:
- Channel point rewards  
- Chat commands  
- Any user-generated input (`rawInput`)  

---

## ✨ Features

- 🔍 Scans user input for bad/swear words  
- 🚫 Replaces detected words with `***` (matching length)  
- 🧠 Case-insensitive detection  
- ✅ Only replaces full words (not inside other words)  
- 📦 Outputs a clean version of the message to a new argument  

---

## ⚙️ How It Works

1. Streamer.bot passes user input through the `rawInput` argument  
2. Script scans the message for bad words  
3. Each detected word is replaced with `*` characters  
4. The filtered message is saved to: badwordsreplaced
5. You can then use this cleaned message in other actions  

---

## 🧩 Requirements

Before running this script:

- You **must create an argument** in Streamer.bot: badwordsreplaced

- 
---

## 🚀 Setup Instructions

1. Open **Streamer.bot**  
2. Create or edit an Action  
3. Add a **C# Sub-Action**  
4. Paste the script below  
5. Make sure your trigger provides: rawInput
6. (Optional) Add a Set Argument before the script: badwordsreplaced = ""


---

## 📥 Usage Example

### Input (rawInput): this is fucking bad
### Output (badwordsreplaced): this is ******* bad



---

## 🧠 Supported Bad Words

Default list included in the script:
fuck
fucking
fucked
shit
bitch
asshole
dick
pussy
cunt
slut
whore
fag
faggot
retard
👉 You can easily edit this list inside the script.

----


⚠️ Notes

- This script does not use regex (avoids Streamer.bot dependency issues)
- Word matching respects boundaries (no partial word replacements)
- You can expand the filter list as needed


-----

💡 Tips

Use badwordsreplaced in:

- Overlays

- TTS systems

- Chat responses

- Combine with moderation tools for stronger filtering


-----

📜 License

Free to use, modify, and share.

This version will paste perfectly into GitHub with no formatting issues 👍

If you want next level, I can also:
- add badges (downloads, version, etc.)
- add screenshots
- or make it look like a top-tier open source repo 🔥


-----

## 💻 Script
```bash
using System;
using System.Collections.Generic;

public class CPHInline
{
    public bool Execute()
    {
        try
        {
            string input = "";
            CPH.TryGetArg("rawInput", out input);
            input = input ?? "";

            List<string> badWords = new List<string>
            {
                "fuck",
                "fucking",
                "fucked",
                "shit",
                "bitch",
                "asshole",
                "dick",
                "pussy",
                "cunt",
                "slut",
                "whore",
                "fag",
                "faggot",
                "retard"
            };

            string output = input;

            foreach (string word in badWords)
            {
                output = ReplaceWord(output, word);
            }

            CPH.SetArgument("badwordsreplaced", output);
            CPH.LogInfo("[Filter] " + output);

            return true;
        }
        catch (Exception ex)
        {
            CPH.LogError("[Filter ERROR] " + ex.ToString());
            return false;
        }
    }

    private string ReplaceWord(string text, string word)
    {
        int index = 0;

        while (true)
        {
            index = text.IndexOf(word, index, StringComparison.OrdinalIgnoreCase);
            if (index == -1) break;

            bool startOk = index == 0 || !char.IsLetter(text[index - 1]);
            bool endOk = (index + word.Length >= text.Length) || !char.IsLetter(text[index + word.Length]);

            if (startOk && endOk)
            {
                string stars = new string('*', word.Length);
                text = text.Substring(0, index) + stars + text.Substring(index + word.Length);
                index += stars.Length;
            }
            else
            {
                index += word.Length;
            }
        }

        return text;
    }
}


