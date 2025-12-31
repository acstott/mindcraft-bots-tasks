# 🧠 Mindcraft Custom Tasks

This repository contains **custom task definitions** intended to be used *with* the  
[Mindcraft](https://github.com/mindcraft-bots/mindcraft) project.

Tasks are written in JSON and define **explicit, goal-oriented missions** for Minecraft AI bots, such as gathering resources, crafting tools, building structures, or delivering items to a player.

> ⚠️ **Important:**  
> This repository contains **tasks only**. You must clone the main **Mindcraft** repository separately to run them.

---

## 🚀 Getting Started (Using These Tasks with Mindcraft)

To use the tasks in this repository, follow these steps:

### 1️⃣ Clone the Mindcraft Repository

```bash
git clone https://github.com/mindcraft-bots/mindcraft.git
cd mindcraft
npm install
```

This sets up the Mindcraft runtime, bot logic, and Minecraft integration.

---

### 2️⃣ Clone or Download This Tasks Repository

You can either clone this repo or download it as a ZIP:

```bash
git clone https://github.com/acstott/mindcraft-bots-tasks
```

---

### 3️⃣ Copy or Reference Tasks into Mindcraft

Inside the Mindcraft repo, tasks are loaded from the `tasks/` directory.

You have two options:

#### Option A: Copy Tasks (Simplest)

```bash
cp -r mindcraft-bots-tasks/tasks/* mindcraft/tasks/
```

#### Option B: Symlink Tasks (Recommended for Development)

```bash
ln -s mindcraft-bots-tasks/tasks mindcraft/tasks/custom
```

This allows you to update tasks here without copying files repeatedly.

---

## ▶️ Running a Task

From inside the **Mindcraft** repository:

```bash
node main.js   --task_path tasks/custom/butter.json   --task_id deliver_gold_block
```

- `--task_path` → path to the JSON file inside Mindcraft
- `--task_id` → the task key inside that file

The bot will connect to the Minecraft world and begin executing the task instructions.

---

## ❓ What Is a Task?

A **task** tells a Mindcraft bot:

- **What the final goal is**
- **How to achieve it step by step**
- **What items are required**
- **How long it is allowed to take**

Tasks are especially useful for:

- Experiments (bot vs human comparisons)
- Demos
- Repeatable challenges
- Educational projects (AI planning, autonomy, tool use)

---

## 📁 File Structure

Custom tasks are stored as JSON files under the `tasks/` directory.

Example:

```text
tasks/
├── butter.json
├── speedrun_tasks.json
└── trial_chamber.json
```
---

## 📝 Task JSON Structure

Here is a typical task definition:

```json
{
  "example_task": {
    "goal": "Human-readable description of what the bot should accomplish.",
    "instructions": [
      "Step-by-step instructions guiding the bot.",
      "Be explicit and concrete."
    ],
    "initial_inventory": {},
    "agent_count": 1,
    "target": "minecraft_item_id",
    "number_of_target": 1,
    "type": "techtree",
    "max_depth": 4,
    "depth": 0,
    "timeout": 900,
    "blocked_actions": {
      "0": [],
      "1": []
    },
    "missing_items": [],
    "requires_ctable": true
  }
}
```

### 🏞️ Field Reference

| Field | Description |
|------|------------|
| `goal` | High-level description of success |
| `instructions` | Explicit, ordered steps the bot should follow |
| `initial_inventory` | Items the bot starts with |
| `agent_count` | Number of bots used |
| `target` | Primary item or outcome |
| `number_of_target` | Quantity required |
| `type` | Planning strategy (`techtree` is recommended) |
| `timeout` | Max execution time in seconds |
| `requires_ctable` | Whether a crafting table is required |

---

## 🧈 Example: Butter Robot 

This task forces the bot to:

- Craft tools (wood → stone → iron)
- Mine and smelt gold
- Craft **1 gold block (9 ingots)**
- Deliver it to the nearest player

```json
{
  "deliver_gold_block": {
    "goal": "Craft the required tools, mine and smelt enough gold to craft one gold block, then deliver the gold block to the nearest player.",
    "instructions": [
      "1. Collect at least 8 logs from nearby trees.",
      "2. Craft the logs into wooden planks.",
      "3. Craft a crafting table.",
      "4. Craft a wooden pickaxe.",
      "5. Mine stone and collect at least 12 cobblestone.",
      "6. Craft a stone pickaxe.",
      "7. Mine iron ore and collect at least 3 raw iron.",
      "8. Craft a furnace.",
      "9. Smelt raw iron into iron ingots.",
      "10. Craft an iron pickaxe.",
      "11. Locate a cave or underground area below Y=32.",
      "12. Mine gold ore until at least 9 raw gold is collected.",
      "13. Smelt raw gold into 9 gold ingots.",
      "14. Craft 1 gold block using the 9 gold ingots.",
      "15. Locate the nearest player.",
      "16. Walk to the player and drop the gold block in front of them."
    ],
    "initial_inventory": {},
    "agent_count": 1,
    "target": "gold_block",
    "number_of_target": 1,
    "type": "techtree",
    "max_depth": 4,
    "depth": 0,
    "timeout": 1800,
    "blocked_actions": {
      "0": [],
      "1": []
    },
    "missing_items": [],
    "requires_ctable": true
  }
}
```

---

## ✅ Best Practices

- Be explicit — vague instructions lead to wandering bots
- Respect Minecraft mechanics (tool requirements, smelting, Y-levels)
- Use realistic timeouts for mining-heavy tasks
- Prefer step-by-step instructions over abstract goals

---

## ⚠️ Common Issues

- Bot gets stuck → instructions are too vague
- Task times out → timeout too low or difficult terrain/pathfinding
- Wrong item names → use exact Minecraft item IDs (e.g. `gold_block`)

---

## 🧪 Educational & Experimental Use

These tasks are well suited for:

- AI planning demonstrations
- Human vs bot speed comparisons
- Science fair projects
- Minecraft automation experiments

---

## ⛏️ References

- Mindcraft repository: https://github.com/mindcraft-bots/mindcraft
- Mineflayer (bot engine): https://github.com/PrismarineJS/mineflayer

---

