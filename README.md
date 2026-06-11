# HexDecBin

A single-file web app for converting between **binary**, **decimal**, and **hexadecimal**, with a clear per-bit visualization and a side-by-side compare mode for two values.

## Usage

Open [index.html](index.html) in any modern browser — no build, no server.

### Single mode

- Type into any of the three inputs (decimal, hex, binary) and the other two update live.
- The binary value is rendered as a row of bit cells, grouped into nibbles. Each nibble shows its hex digit and bit-range label (e.g. `A [15:12]`).
- Hover any bit to see its index and place value (`2^N`).
- Width selector (8/16/32/64/128-bit, or auto) controls how many bits are shown. If the value needs more bits than the selected width, it auto-expands.

### Compare mode

- Toggle to **Compare** at the top to enter two values (A and B) at once.
- Bit visualizations for A and B are stacked and column-aligned at the same width.
- Bits where A and B differ are outlined in red on both rows.
- An additional `A ⊕ B` row marks differing positions with `×` and matching ones with `·`. A "_N bits differ_" summary appears in the controls bar.

### Saved values

- Use the sidebar to save the current value (optionally with a name) into `localStorage` so it persists across reloads.
- Saved entries can be **pinned** into a slot:
  - **Single mode**: click an entry's row to pin it as the value; click again to unpin (clears the input).
  - **Compare mode**: each entry has small **A** and **B** toggle buttons. Click to pin that entry as the A or B value; click again to unpin. Active pins are highlighted in the slot's color.
- Typing into an input unpins that slot, since the value no longer matches the saved entry.
- Saving a value that already exists pins the existing entry instead of creating a duplicate; if you typed a new name, the existing entry is renamed.

## Notes

- Values are handled as `BigInt`, so conversions stay precise up to 128+ bits.
- Hex accepts an optional `0x` prefix; binary tolerates spaces and underscores.
- Negative values are not supported.

## Future ideas

Things considered but not built yet, roughly in order of impact:

- **Persist UI state across reloads** — current mode (single/compare), width selector, and `activeIdx` pins reset on every load. Saves themselves already persist.
- **Bitwise operations between A and B** — surface `A & B`, `A | B`, `A ^ B` (already implicit in the diff row), `~A`, plus shifts, as additional rows in compare mode.
- **Two's-complement / signed support** — handle negative inputs and a sign-aware width display.
- **Edit and reorder saved entries** — inline rename, drag-to-reorder, plus export/import as JSON.
- **Save-button state in single mode** — `Save B` is hidden via CSS in single mode but still `enabled` in the DOM if B has a value from before the mode switch. Functionally fine since it's unreachable, but worth cleaning up if B is later exposed in other ways.
- **Tooltip clipping at panel edges** — the bit-cell tooltip can be cut off on the leftmost/rightmost bit because the viz panel uses `overflow-x: auto`. A JS-positioned tooltip would fully fix it.
- **Round-up to standard widths in auto mode** — auto-expansion currently rounds up to the next multiple of 4, so a 33-bit value renders as 36 bits. Snapping to the next standard width (32 → 64 → 128) would be tidier.
- **Responsive layout** — the sidebar is a fixed 280px column. On narrow viewports it would benefit from collapsing or moving below the main column.
- **Keyboard / a11y polish** — add `aria-pressed` on the pin toggles, `role="radiogroup"` on the mode toggle, focus styles on the per-entry buttons.
