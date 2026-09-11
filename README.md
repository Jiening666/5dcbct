# Cardiorespiratory 5D-CBCT — results viewer

Interactive companion to *Cardiorespiratory 5D-CBCT from a routine one-minute acquisition*.

**[Open the viewer →](https://jiening666.github.io/5dcbct/)**

Three clinical Halcyon HyperSight acquisitions (866 projections, ~60 s, no additional imaging
dose) compared across four reconstructions on one common grid, one common intensity scale and
one display window:

| | state | views per output |
|---|---|---|
| **Proposed 5D** | continuous respiratory × cardiac | all 866, every state |
| Static Gaussian | none | all 866 |
| Unbinned FDK | none | all 866 |
| Respiratory-binned FDK | 10 discrete respiratory bins | 77–96 |
| Dual-gated FDK | 10 × 6 respiratory × cardiac bins | 7–23 |

The proposed reconstruction is shown alone by default; **Show beside ours** adds any baseline
next to it. Pick a patient and a plane, step through five slices with the slider, the mouse
wheel or the arrow keys, and move respiratory and cardiac state independently.

Both binned FDKs carry their own state and are shown with it — a bin per stop — because
freezing them at one bin would understate them. What they cannot do is sit between bins, and
the cardiac axis costs them an order of magnitude in views.

### How it renders

No server, no renderer, no GPU. Each fitted model was queried offline on a 10 × 6 grid of
respiratory × cardiac states, for every plane and slice, and the results packed into one sprite
sheet per (plane, slice); the binned FDKs were reconstructed once per bin and packed the same
way. Moving a state slider pans a sheet with CSS. The page itself is 27 KB and fetches only the
images it is showing.

A **signal extraction** section plays the per-frame QA video for each case: the projection with
the tracked landmarks drawn on it, those surrogates band-passed and fused, and the respiratory
and cardiac traces the reconstruction was actually driven by.

```
index.html          the page
static/style.css    styling
assets/             480 baked panels and sprite sheets, 3 QA videos, the method figure
assets/index.json   plane, slice and window metadata for the bake
```

### Notes

Patients are de-identified and acquisition dates removed. Patient-domain metrics are
projection-domain fit metrics — the claim that recovered motion is physically correct rests on
the twelve-case XCAT phantom study, where volumetric ground truth exists.
