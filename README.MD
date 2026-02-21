# Autodesk Maya – MEL Scripts
A collection of MEL scripts for Autodesk Maya focused on skinning and
rigging workflows.

<div align="center">
    <img src="assets/raptile_bytez_logo.png" alt="Raptile Bytez Logo" width="250">
    <br>
    <img src="assets/rigging_banner.png" alt="Raptile Bytes Rigging Banner" width="100%">
</div>

---

## Scripts

### FiveOrMore.mel

Selects all vertices of a skinned mesh that are influenced by **more than
4 joints** (configurable). The result is displayed as a vertex selection
directly in the viewport, making it easy to visually identify and
manually fix problematic areas.

**Use case:** Quality check before export – quickly find vertices that
exceed the maximum influence count required by game engines or rigs.

**Parameters (edit at the top of the script):**

| Parameter | Default | Description |
|---|---|---|
| `$weightTolerance` | `0.001` | Minimum weight to count as active influence |
| `$maxInf` | `4` | Maximum allowed number of active influences |

**Usage:**
1. Select exactly one skinned mesh (Transform node) in the viewport
2. Run the script in the Maya Script Editor
3. All violating vertices are selected and highlighted
4. The number of affected vertices is printed to the Script Editor output

---

### FourMax.mel

Automatically **prunes** all vertices of a skinned mesh down to a maximum
of 4 active influences (configurable). Uses a Bubble Sort to identify the
weakest influences per vertex and removes them via `skinPercent -pruneWeights`,
then normalizes the remaining weights automatically.

**Use case:** Automated cleanup for game-ready assets – enforce strict
influence limits across an entire mesh in one step.

**Parameters (edit at the top of the script):**

| Parameter | Default | Description |
|---|---|---|
| `$MaxInfluence` | `4` | Maximum allowed number of active influences |
| `$weightTolerance` | `0.0001` | Minimum weight to count as active influence |

**Usage:**
1. Select exactly one skinned mesh (Transform node) in the viewport
2. Run the script in the Maya Script Editor
3. The script processes every vertex automatically
4. A summary report is printed to the Script Editor output

---

## Recommended Workflow

Run **FourMax.mel** first to automatically prune all violations, then
run **FiveOrMore.mel** afterwards to verify that no violating vertices
remain.

---

## Requirements

- Autodesk Maya (tested with Maya 2020+)
- MEL Script Editor or a shelf button

## Author

**Jesco Wurm** – [RaptileBytez](https://github.com/RaptileBytez)

---

## License

This project is licensed under the MIT License.
See [LICENSE](LICENSE) for details.
