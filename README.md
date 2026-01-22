# Step Name Plot

Interactive Plotly utility to visualize GameObject trajectories grouped by `stepName` and VR variant.

## Features
- Builds one subplot per `stepName`, 2 columns auto-layout.
- Overlays trajectories per `VR` (color-coded) and `stepIndex`; legends toggle all traces per VR via `legendgroup`.
- Equal X/Z scales and shared axes ranges to avoid distortion.
- Trims first/last second of each step, drops zeroed positions, sorts by trial and step.
- Exports a self-contained HTML per data subfolder using Plotly CDN.

## Data requirements
CSV files must include at least these columns:
- `Current Time` (datetime), `CurrentTrial` (int), `CurrentStep` (int), `stepName` (string),
- `stepIndex` (int), `VR` (string), `GameObjectPosX`, `GameObjectPosZ` (float).

## Usage
```bash
# all subfolders
python plot_by_stepname.py /path/to/data_root

# only newest subfolder (fast for testing)
python plot_by_stepname.py /path/to/data_root --latest-only
# also accepts `-latest-only` or `-L` as shorthand
```
- `data_root` should contain subfolders with the CSV logs; each subfolder outputs `<subfolder>_ant_positions_by_step.html` inside it.
- Optional: `--trim-seconds 0.5` to change leading/trailing trim.

## Environment
- Python 3.10+
- Install deps: `pip install -r requirements.txt`

## Next steps
- Re-test legend toggling; if still stuck, inspect generated HTML for legendgroup handling and consider refactoring with Plotly Express facets or Dash.
