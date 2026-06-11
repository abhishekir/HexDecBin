# HexDecBin

A single-file web app for converting between **binary**, **decimal**, and **hexadecimal**, with a clear per-bit visualization.

## Usage

Open [index.html](index.html) in any modern browser — no build, no server.

- Type into any of the three inputs and the other two update live.
- The binary value is rendered as a row of bit cells, grouped into nibbles. Each nibble shows its hex digit and bit-range label (e.g. `A [15:12]`).
- Hover any bit to see its index and place value (`2^N`).
- Width selector (8/16/32/64/128-bit, or auto) controls how many bits are shown. If the value needs more bits than the selected width, it auto-expands.

## Notes

- Values are handled as `BigInt`, so conversions are precise up to 128+ bits.
- Hex accepts an optional `0x` prefix; binary tolerates spaces and underscores.
- Negative values are not supported.
