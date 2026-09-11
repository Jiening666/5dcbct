# Cardiorespiratory 5D-CBCT — results viewer

Interactive companion to *Cardiorespiratory 5D-CBCT from a routine one-minute acquisition*.

**[Open the viewer →](https://jiening666.github.io/5dcbct/)**

Three clinical Halcyon HyperSight acquisitions (866 projections, ~60 s, no additional imaging
dose) compared across four reconstructions on one common grid, one common intensity scale and
one display window:

| | |
|---|---|
| Unbinned FDK | all 866 views, no motion state |
| Respiratory-binned FDK | ~80 views per bin, 10 bins |
| Static Gaussian | all views, motion-averaged |
| **Proposed 5D** | continuous respiratory–cardiac state |

Pick a patient and a plane, step through five slices per plane with the slider or the mouse
wheel, and move respiratory and cardiac state independently. Only the 5D panel responds to
state — the three baselines have no state to move.

### How it renders

No server, no renderer, no GPU. Each fitted model was queried offline on a 10 × 6 grid of
respiratory × cardiac states, for every plane and slice, and the results packed into one sprite
sheet per (plane, slice); moving a state slider pans that sheet with CSS. The page itself is
23 KB and fetches only the images it is showing.

```
index.html          the page
static/style.css    styling
assets/             420 baked panels and sprite sheets + the method figure
assets/index.json   plane, slice and window metadata for the bake
```

### Notes

Patients are de-identified and acquisition dates removed. Patient-domain metrics are
projection-domain fit metrics — the claim that recovered motion is physically correct rests on
the twelve-case XCAT phantom study, where volumetric ground truth exists.
