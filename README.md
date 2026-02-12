# Visual Dialog Editor

A robust, single-file visual editor for creating branching narratives, game dialogues, and interaction logic. Built entirely with Vue 3, it requires no installation, no build servers, and no external dependencies—just download and run.

## ✨ Key Features

* **Zero Setup:** It is a single HTML file. Open it in any modern browser to start working.
* **Visual Node Graph:**
    * Drag-and-drop workflow with infinite canvas (pan/zoom).
    * **Flow Nodes:** Start, End, and Branching logic.
    * **Logic Nodes:** Set/Get variables and compare values (Int, Float, String, Bool).
    * **Grouping:** Organize complex trees with visual groups.
* **Localization First:**
    * Built-in support for multiple languages.
    * CSV Import/Export for translators.
    * Voice Actor Script generation (CSV).
* **Production Ready:**
    * **Project JSON:** Saves your complete workspace state.
    * **Runtime JSON:** Exports a stripped-down, optimized JSON structure ready to be parsed by your Game Engine (Unity, Godot, Unreal, Custom).
* **Smart Validation:** Real-time error checking for disconnected nodes, missing translations, or invalid variable references.

## 🚀 Getting Started

1.  Download the `Dialog-Editor.html` file from this repository.
2.  Open the file in Chrome, Firefox, or Edge.
3.  Start creating!

## 🛠 Workflow

1.  **Create Characters:** Define speakers with custom colors and variables in the sidebar.
2.  **Define Variables:** Set up global state flags (e.g., `hasMetKing`, `goldAmount`).
3.  **Build the Graph:** Connect `Start` nodes to `Text` nodes. Add `Choices` to text nodes to create branching paths.
4.  **Add Logic:** Use `Compare` nodes to check variables and route flow (e.g., *if Gold > 50, show secret shop*).
5.  **Export:**
    * Save your work via **Project JSON**.
    * Export for your game via **Runtime JSON**.

## 📦 Runtime Data Format

The editor exports a clean, engine-agnostic JSON format designed for easy parsing.

**Example Structure:**
```json
{
  "globalVars": {
    "isTutorialFinished": { "type": "bool", "value": "false" }
  },
  "dialogs": [
    {
      "id": 1,
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
              "translations": { "en": "Hi!", "de": "Hallo!" }
            }
          ]
        }
      ],
      "connections": [
        { "from": 101, "fromSocket": "out_ans_0", "to": 102, "toSocket": "in" }
      ]
    }
  ]
}