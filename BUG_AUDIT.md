# Watermark Studio v2.3.3 Bug Audit

## Fixed

### Brand layout: swap primary/secondary content

Previous behavior only swapped the internal primary/secondary mapping roles. The actual text order in the canvas and the text editor remained unchanged, so a document such as:

- Primary: FINN
- Secondary: AIGC

could still show `FINN / AIGC` after pressing the swap button.

v2.3.3 changes the button semantics to **Swap primary/secondary content**:

1. The actual mapped text lines are swapped.
2. The text editor updates immediately.
3. The canvas updates immediately.
4. Primary/secondary layout roles are recalculated with the current brand layout preset.
5. Character-level font/color styles follow their text content.
6. Per-line optical offsets follow their text content.
7. Undo/Redo history records the full operation.

Example:

Before:
```
FINN
AIGC
```
Primary = FINN, Secondary = AIGC

After **Swap primary/secondary content**:
```
AIGC
FINN
```
Primary = AIGC, Secondary = FINN

## Static checks

- JavaScript syntax: passed (`node --check`)
- Brand swap control: present
- Current brand preset is reapplied after swap without replacing text with placeholders
