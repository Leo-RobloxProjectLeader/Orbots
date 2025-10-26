# 🧩 Orbots  
*A structured and readable organization standard for Roblox Lua scripts.*

[![Made for Roblox](https://img.shields.io/badge/Made%20for-Roblox-red?style=flat-square)]()
[![Lua](https://img.shields.io/badge/Language-Lua-blue?style=flat-square)]()

---

## 📘 Overview

**Orbots** (short for **O**versimplified **R**oblox **O**rganized **T**ype **S**cript) is a structured organization system designed to make Roblox Lua scripts **cleaner, easier to read**, and **more consistent** across large projects.

It’s not a new programming language — it’s a **scripting style and formatting standard** that helps developers maintain organization and readability when working on complex Roblox experiences.

---

## ⚙️ Script Naming Convention

Each Orbots script follows this structure: <runtime>-<id>-<type>.orbots

| Part | Description | Example |
|------|--------------|----------|
| `runtime` | Either `server` or `client`, depending on where the script runs | `server` |
| `id` | Script ID. Goes `A1 → A9`, then continues alphabetically (`B1`, `C1`, …). After `Z9`, restart with `1A1`, `1A2`, etc. | `A2` |
| `type` | Script type: `m` = Module Script, `nm` = Non-Module Script | `nm` |

**Example filename:**

server-A2-nm.orbots

Each script must also include a **StringValue attribute** named `RealName` — this stores the readable name of the script (e.g., `"Controller"`).

---

## 🧱 Section Headers

Sections are divided with **comment tags** to improve readability.  
In Orbots, Lua comments are used like this:

--#SECTION_NAME#--


### Available Sections

| Section | Purpose |
|----------|----------|
| `IMPORTS` | Service references, `require()` calls |
| `VARIABLES` | Variable and constant declarations |
| `FUNCTIONS` | Function definitions |
| `EVENTS` | Event connections |
| `MAIN LOOP` / `CORE LOOP` / `GAME LOOP` | Main logic loops |
| `BASECODE` | Initialization or startup logic |
| `UNCATEG` | Miscellaneous or temporary code |

**Rules:**
- Section names are **UPPERCASE**.  
- Always have **one blank line below** each section header.  
- Empty sections should include a comment placeholder (e.g. `-- No functions yet`).

---

## 🔠 Naming Conventions

| Type | Case | Example |
|------|------|----------|
| Variables | `camelCase` | `playerHealth` |
| Constants | `ALL_CAPS` | `MAX_SPEED` |
| Functions | `PascalCase` | `ReturnPlayerHp()` |
| Parameters | `snake_case` | `player_id` |
| Script RealName | `PascalCase` | `Controller` |

---

## ✏️ Spacing & Indentation Rules

### Equal Signs

Exactly **one space** before and after `=`.

```lua
local speed = 16
```

### Commas

One space **after**, none **before**.

```lua
print(a, b, c)
```

### Parentheses

No spaces inside parentheses or before opening one.

```lua
print(x)
ReturnPlayerHp(player_id)
```

### Operators

One space around binary operators.

```lua
if a + b == c then
```

No space for unary operators.

```lua
not a
```

---

### Indentation

Use one tab (or 4 spaces) per scope level.
```end``` must align with its opening statement.

```lua
if condition then
	print("Indented")
end
```

## 🧩 Scope Spacing Rules

Always include **one blank line** before starting a control structure (```if```, ```for```, ```while```, ```repeat```, ```function```).

### ✅ Correct:

```lua
local function ReturnHp(hp_value: NumberValue)
	local tempValue = hp_value
	
	if tempValue.Value > 50 then
		print("High HP")
	end
end
```

### ❌ Incorrect:

```lua
local function ReturnHp(hp_value: NumberValue)
	local tempValue = hp_value
	if tempValue.Value > 50 then
		print("High HP")
	end
end
```

## ⚡ One-Line if Rules

Only allowed when performing short, direct control actions such as:

```lua
return
  
break
  
continue
  
error()
```

### ✅ Allowed:

```lua
if exampleValue == 0 then return end
if not player then return end
```

### ❌ Not allowed:

```lua
if tempValue == 0 then print("Zero") end
if tempValue > 10 then tempValue -= 1 end
```

### Rules:

**1.** The statement must perform a single, short action.

**2.** There must be **exactly one space** before and after each keyword (```if```, ```then```, ```end```).

**3.** Never chain multiple one-line ```if``` statements.

**4.** Do not use for logic other than flow control.

---

## 💬 Comment Rules

One space after ```--```.

```lua
-- This is a comment
```

Multiline comments:

```lua
--[[
	This is a multi-line comment block
]]--
```

Comments must align with code indentation.

Avoid unnecessary comments — focus on clarity.

---

## 🧠 Example Script:

```lua
-- server-A2-nm.orbots
-- RealName: "Controller"

--#IMPORTS#--
local Players = game:GetService("Players")

--#VARIABLES#--
local playerHealth = 100
local MAX_SPEED = 32

--#FUNCTIONS#--
local function ReturnPlayerHp(player_id)
	local tempValue = playerHealth
	
	if not tempValue then return end
	if tempValue == 0 then return end
	
	if tempValue > 50 then
		print("High HP")
	end
end

--#EVENTS#--
Players.PlayerAdded:Connect(function(player)
	print(player.Name .. " joined")
end)
--#MAIN LOOP#--

while task.wait(1) do
	print("Running main logic...")
end

--#BASECODE#--
print("Controller initialized.")
```

---

## 🧭 Future Plans

```.orbotsconfig``` file for custom rule definitions

```.orbots-gen``` tool for auto-generating script templates

Linter/formatter to enforce Orbots standards automatically

---

## 🪪 License

This project is open for personal and collaborative use.
You are free to **adapt**, **extend**, and **contribute** to the Orbots standard — just keep credits intact where appropriate.

## 📚 Table of Contents
- [Overview](#-overview)
- [Script Naming Convention](#-script-naming-convention)
- [Section Headers](#-section-headers)
- [Naming Conventions](#-naming-conventions)
- [Spacing & Indentation Rules](#-spacing--indentation-rules)
- [Scope Spacing Rules](#-scope-spacing-rules)
- [One-Line if Rules](#-one-line-if-rules)
- [Comment Rules](#-comment-rules)
- [Example Script](#-example-script)
- [Future Plans](#-future-plans)
- [License](#-license)
