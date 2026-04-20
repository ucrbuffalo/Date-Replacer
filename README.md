# Date Replacer (Alfred Workflow)

A configurable Alfred workflow that inserts dates using quick snippet triggers—ideal for logging, filenames, tickets, and notes.  
Supports:

- **Next weekday** (e.g., next Tuesday)
- **Last weekday** (e.g., last Monday)
- **Relative days** (yesterday / today / tomorrow)
- **User-configurable output format** via Alfred’s Configuration Builder

---

## Requirements

- Alfred (Powerpack may be required for snippet triggers and workflows)
- macOS with AppleScript support (built-in)

---

## Installation

1. Download the workflow file: `Date Replacer.alfredworkflow`
2. Double-click to import into Alfred.
3. Open **Alfred Preferences → Workflows → Date Replacer**
4. (Optional) Configure the output date format:
   - Click the workflow’s “Configure Workflow…” button
   - Choose your preferred **Date Format** from the dropdown

---

## Configuration (Date Format)

This workflow uses a configuration variable named:

- `dateFormat`

You can choose one of the following format options:

- `Weekday, Month D, YYYY` 	(example: `Tuesday, April 21, 2026`)
- `DD-MM-YYYY` 				(example: `21-04-2026`)
- `MM-DD-YYYY` 				(example: `04-21-2026`)
- `YYYY-MM-DD` 				(example: `2026-04-21`)
- `DD/MM/YYYY` 				(example: `21/04/2026`)
- `MM/DD/YYYY` 				(example: `21/04/2026`)
- `YYYY/MM/DD` 				(example: `2026/04/21`)
- `DDMMYYYY` 					(example: `21042026`)
- `MMDDYYYY` 					(example: `04212026`)
- `YYYYMMDD` (**default**) 			(example: `20260421`)

If `dateFormat` is not set, the workflow defaults to:

- `YYYYMMDD`

---

## Usage

### A) Next weekday triggers (examples)

Type one of the snippet triggers below to paste the **next** occurrence of that weekday:

- `//mon` → next Monday
- `//tue` → next Tuesday
- `//wed` → next Wednesday
- `//thu` → next Thursday
- `//fri` → next Friday
- `//sat` → next Saturday
- `//sun` → next Sunday

> “Next” is strictly in the future: if today is Tuesday and you trigger `//tue`, it returns **next week’s Tuesday**.

---

### B) Last weekday triggers (examples)

Type one of the snippet triggers below to paste the **previous** occurrence of that weekday:

- `//lmon` → last Monday
- `//ltue` → last Tuesday
- `//lwed` → last Wednesday
- `//lthu` → last Thursday
- `//lfri` → last Friday
- `//lsat` → last Saturday
- `//lsun` → last Sunday

> “Last” is strictly in the past: if today is Monday and you trigger `//lmon`, it returns **last week’s Monday**.

---

### C) Relative day triggers (examples)

Type one of the snippet triggers below to paste a relative date:

- `//yest` → yesterday
- `//date` → today
- `//today` → today
- `//tom` → tomorrow

All outputs respect the configured `dateFormat`.

---

## Examples

Assume `dateFormat = ymd_compact` and today is April 20, 2026:

- `//today` → `20260420`
- `//tom` → `20260421`
- `//yest` → `20260419`
- `//ltue` → `20260414` (last Tuesday)
- `//tue` → `20260421` (next Tuesday)

If `dateFormat = long_full`:

- `//date` → `Monday, April 20, 2026`

---

## How It Works (for tinkerers)

- Snippet triggers fire workflow branches.
- Each branch sets a variable (e.g., `targetDay` or `offsetDays`).
- AppleScript computes the target date using macOS date arithmetic.
- Output is formatted based on the `dateFormat` config value.
- A newline-stripping step ensures clean paste behavior.

---

## Customization

### Add new triggers
To add a new snippet trigger:
1. Duplicate an existing snippet trigger object
2. Update the trigger text (e.g., `//lnextmon`)
3. Update its variable assignment (`targetDay` or `offsetDays`)
4. Connect it into the same script/output chain

### Change behavior to “include today”
By default:
- “Next weekday” skips today if it matches (returns next week)
- “Last weekday” skips today if it matches (returns last week)

If you want “include today” behavior, adjust the delta logic in the AppleScript:
- For “next”: change `if delta is 0 then set delta to 7` to `set delta to 0`
- For “last”: change `if delta is 0 then set delta to 7` to `set delta to 0`

---

## AI Disclosure

I used Copilot extensively in this project. Enough so that I would consider it "vibe coded".
These scripts do not call for information on the internet, nor send your data to the internet.

---

## License

This project is licensed under the MIT License, which permits use, modification,
and redistribution with attribution.

Note: Third‑party trademarks/icons are not covered by this license.

See the [`LICENSE.txt`](./LICENSE.txt) file for the complete license text.

---

## Credits

Built by: **ucrbuffalo**  
Workflow: **Date Replacer**  
Bundle ID: `com.cameronphillips.datereplacer`
Powered by: Alfred + AppleScript
