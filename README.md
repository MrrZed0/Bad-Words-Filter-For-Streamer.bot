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
4. The filtered message is saved to:
