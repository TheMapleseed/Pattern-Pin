# Pattern Pin

**Mapleseed Inc.**  
Copyright © 2026 Mapleseed Inc. All rights reserved.

Pattern Pin is a proprietary device-unlock design owned by Mapleseed Inc. The owner of a device remembers a gesture. The device keeps the symbols that gesture crossed when the lock was created, and uses those symbols as the seed of a private key. Each time the lock is shown, that private key produces a new public pin sequence for that presentation only. The same gesture reads the sequence back. The presentation is wiped when the display turns off or the device unlocks.

This is not an open specification and it is not licensed for implementation. Possession of this repository does not grant any right to use, implement, reproduce, modify, or distribute the work. Written permission from Mapleseed Inc. is required.

## Repository

| File | Role |
| --- | --- |
| [`PatternPin.tex`](PatternPin.tex) | Normative specification. Mapleseed Inc. property. |
| [`PatternPin.pdf`](PatternPin.pdf) | Built paper. Rebuild it from the TeX source after any change. |

The paper is the specification. This page is the project description. Normative parameters, record layout, and the worked example live in the paper.

## Design

Pattern Pin is the hybrid of a pattern lock and a PIN lock.

A pattern lock asks for a path on a fixed grid. A PIN lock asks for a string on a fixed keypad. Here the person remembers the path. The symbols under the path change on every presentation, and the private key never appears on the glass.

Enrollment shows one randomly placed symbol per cell, on a 3×3 or a 4×4 grid. The gesture is confirmed by drawing it twice. The ordered symbols under that gesture are the pin contents. Those contents generate the private key. The cell sequence of the gesture is kept separately, as the layout pattern, so later grids can be built for the same path. The enrollment grid is discarded.

A lock presentation draws a nonce that exists only for that presentation. The private key and the nonce expand into a public pin sequence. The layout pattern places that sequence on the grid, and the remaining cells are filled around it. The phone hashes the symbols the repeated gesture actually reads and compares that digest with the public hash of the sequence it just generated. A match authorizes one use of the private key to unwrap the device key. The nonce, the public sequence, the public hash, and the grid are then wiped. The next time the display comes on, a different public hash is generated from the same private key.

The sealed record stays in hardware-backed storage. Ordinary applications do not receive the pin contents, the private key, or the unwrapped device key.

## What the construction holds

An observed symbol string dies with the presentation that produced it. A later presentation will not accept it. A picture of one grid does not reveal the private key. There is no standing numeric PIN on the glass.

The gesture itself remains the durable secret the person remembers. Someone who learns the path can draw it on the next grid, because each grid is laid out for that path. Someone who can read the hardware-backed record can derive the private key. The paper states both results in full.

## Build

Rebuilding the paper requires a current TeX Live with `geometry`, `microtype`, `amsmath`, `amssymb`, `booktabs`, `enumitem`, `xcolor`, `tikz`, `fancyhdr`, and `hyperref`.

```sh
pdflatex PatternPin.tex
pdflatex PatternPin.tex
```

The second pass fills the table of contents and the cross-references.

## Rights

Copyright © 2026 Mapleseed Inc. All rights reserved.

No license is granted by this repository. Mapleseed Inc. reserves all rights in the Pattern Pin design, the specification, the figures, and this description.
