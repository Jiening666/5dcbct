# Cardiorespiratory 5D-CBCT — results viewer

Interactive companion to *Cardiorespiratory 5D-CBCT from a routine one-minute acquisition*.

**[Open the viewer →](https://jiening666.github.io/5dcbct/)**

Three clinical Halcyon HyperSight acquisitions (866 projections, ~60 s, no additional imaging
dose) are compared across four reconstructions on one common grid, one common intensity scale
and one display window:

| | |
|---|---|
| Unbinned FDK | all 866 views, no motion state |
| Respiratory-binned FDK | ~80 views per bin, 10 bins |
| Static Gaussian | all views, motion-averaged |
| **Proposed 5D** | continuous respiratory–cardiac state |

Respiratory and cardiac state are adjustable live. Only the 5D column responds — the three
baselines have no state to move.

### How it renders

The page is a single self-contained HTML file with no server, no renderer and no GPU. Each
fitted model was queried offline on a 10 × 6 grid of respiratory × cardiac states and the
slices packed into one sprite sheet per view; moving a slider pans that sheet.

### Notes

Patients are de-identified and acquisition dates removed. Patient-domain metrics are
projection-domain fit metrics — the claim that recovered motion is physically correct rests on
the twelve-case XCAT phantom study, where volumetric ground truth exists.
