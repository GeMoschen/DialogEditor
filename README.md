# Visual Dialog Editor

A robust, single-file visual editor for creating branching narratives, game dialogues, and interaction logic. Built entirely with Vue 3, it requires no installation, no build servers, and no external dependencies—just download and run.

## ✨ Key Features

* **Zero Setup:** It is a single HTML file. Open it in any modern browser (Chrome, Firefox, Edge) to start working immediately.
* **Visual Node Graph:**
    * **Infinite Canvas:** Pan and zoom freely.
    * **Organization:** Drag-and-drop nodes, grid snapping, and box selection.
    * **Grouping:** Use Group nodes to organize complex logic clusters visually.
* **Advanced Logic System:**
    * **Variable Scoping:** Support for **Global** (game-wide), **Character** (entity-specific), and **Dialog** (local/temporary) variables.
    * **Logic Gates:** Full suite of dynamic logic gates (AND, OR, XOR, NAND, NOR) with adjustable input counts.
    * **Conditional Choices:** Create choices that only appear if specific logic conditions are met (e.g., *only show "Bribe Guard" if Gold > 50*).
* **Event System:**
    * **Fire Events:** Trigger external game events (e.g., *PlaySound*, *UnlockAchievement*, *StartQuest*) directly from the dialogue flow.
    * **Dynamic Arguments:** Pass variables, logic results, or conditions as arguments to your events.
* **Localization First:**
    * Built-in support for unlimited languages.
    * **CSV Import/Export:** Seamless workflow for translators to work in Excel/Sheets.
    * **Voice Script Generation:** Export linear CSV scripts specifically formatted for voice recording sessions.
* **Smart Validation:** Real-time error checking highlights disconnected nodes, missing translations, duplicates, or invalid variable references instantly.
* **Production Ready:**
    * **Project JSON:** Saves your complete workspace state (layout, view settings).
    * **Runtime JSON:** Exports a stripped-down, optimized JSON structure ready to be parsed by your Game Engine (Unity, Godot, Unreal, Custom).

## 🧩 Node Types

The editor features a comprehensive set of nodes to handle flow and data:

### Flow & Narrative
* **Start:** The entry point of the dialogue.
* **End:** Terminates the dialogue or switches to a different Dialog ID.
* **Text Node:** The core narrative block.
    * Assign Characters (with custom colors).
    * Define Localization Keys and Audio Notes.
    * Add multiple **Answers/Choices**.
    * Attach **Logic Conditions** to answers to restrict visibility.

### Events
* **Fire Event:** A node to trigger signals to your game engine.
    * Define a custom `Event Name`.
    * Add dynamic `Arguments` to pass data (Variables, Boolean checks) with the event.

### Data & Variables
* **Set Variable:** Modify Global, Character, or Dialog variables (Operations: `=`, `+=`, `-=`).
* **Get Variable:** Retrieve the current value of a variable to use in logic.

### Logic & Branching
* **Compare:** Compare two values (Int, Float, String, Bool) using operators (`==`, `!=`, `<`, `>`, `contains`) to branch the flow (True/False).
* **Logic Gates:** Combine multiple boolean inputs to drive complex logic.
    * **AND / NAND**
    * **OR / NOR**
    * **XOR**
    * *Note: Logic gates support dynamic input counts (add/remove inputs as needed).*

## 🚀 Getting Started

1.  Download the `DialogEditor.html` file from this repository or simply [CLICK HERE](https://gemoschen.github.io/DialogEditor/DialogEditor.html).
2.  Open the file in Chrome, Firefox, or Edge.
3.  Start creating!

## 🛠 Workflow

1.  **Setup:** Define Languages and Global Variables in the sidebar.
2.  **Cast:** Create Characters, assign their specific text colors, and define character-specific variables (e.g., `trustLevel`).
3.  **Local Variables:** Use the top-right overlay to define variables specific to the current dialog (e.g., `loopCount`), with optional "Reset on Start" behavior.
4.  **Graphing:**
    * Connect `Start` nodes to `Text` nodes.
    * Add choices to Text nodes and attach logic to **Conditional Inputs**.
    * Use **Fire Event** nodes to trigger scripts in your engine (e.g., "AddQuestItem").
5.  **Export:**
    * Save your work via **Project JSON**.
    * Export for your game via **Runtime JSON**.

## 📦 Runtime Data Format

The editor exports a clean, engine-agnostic JSON format designed for easy parsing. Logic, conditions, and events are serialized to allow your engine to evaluate them at runtime.

**Example Structure:**
```json
{
  "globalVars": {
    "isTutorialFinished": { "type": "bool", "value": "false" }
  },
  "dialogs": [
    {
      "id": 1,
      "variables": {
        "tempCounter": { "type": "int", "value": "0", "resetOnStart": true }
      },
      "nodes": [
        {
          "id": 101,
          "type": "Text",
          "characterId": 2,
          "textKey": "intro.text.101",
          "translations": { "en": "Hello traveler!", "de": "Hallo Reisender!" },
          "choices": [
            {
              "id": "out_ans_0",
              "textKey": "intro.text.101.c1",
              "translations": { "en": "Hi!", "de": "Hallo!" },
              "conditionNodeId": 205 
            }
          ]
        },
        {
          "id": 105,
          "type": "FireEvent",
          "eventName": "PlaySound",
          "args": [ 301, null ] // References to data nodes (301) connected to Arg 1
        }
      ],
      "connections": [
        { "id": 1, "from": 101, "fromSocket": "out_ans_0", "to": 105, "toSocket": "in" }
      ]
    }
  ]
}