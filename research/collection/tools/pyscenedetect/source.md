# PySceneDetect

Source snapshot: https://github.com/Breakthrough/PySceneDetect (commit-pinned 2026-04-30) and https://www.scenedetect.com.

PySceneDetect is a Python and command-line tool for automatic shot-boundary (scene cut) detection in video files. It is the most widely used open-source scene cut tool and powers preprocessing pipelines for many video annotation systems.

Detection algorithms:

- ContentDetector (default): pixel-level Hue Saturation Value (HSV) frame-difference threshold, suitable for detecting hard cuts.
- AdaptiveDetector: rolling-window adaptive threshold for content detector, robust to slow fades.
- ThresholdDetector: simple intensity threshold, useful for fade-to-black or fade-from-black detection.
- HistogramDetector: histogram-based comparison.
- HashDetector: perceptual-hash-based comparison.

Outputs:

- CSV / TSV / JSON listings of cuts with start / end timestamps and frame indices.
- Optional split into per-shot video files via ffmpeg.
- HTML report with thumbnail per shot.

Common workflow:

```
pip install scenedetect
scenedetect -i input.mp4 detect-content list-scenes save-images
```

The tool handles long-form video (movies, broadcast TV) and produces stable, reproducible outputs given a fixed threshold and detector choice. License: BSD-3-Clause.

Reference (citation form):

Castellano, B. (2014-2024). PySceneDetect: Video Scene Cut Detection and Analysis Tool. Open source Python package. https://github.com/Breakthrough/PySceneDetect.
