# Peg Game Solver

Solves peg solitaire (the Cracker Barrel triangle game) for **any board
size**, producing a move list a person can follow to finish with one peg.

    cargo run 5 1        # standard 15-hole board, position 1 empty
    cargo run 6 4        # 21-hole board — any size ≥ 5, any empty start

## The representation

The board is triangular, but it's stored as a flat 1D array. A board of
side *n* has n(n+1)/2 positions; row and position map to an index with
triangular-number arithmetic, and every legal jump is an index offset
computed from the row geometry rather than a lookup in a 2D structure.

That flattening is what makes arbitrary sizes work: no hardcoded board,
no 2D allocation — move generation is pure index math over contiguous
memory, which also keeps the search fast in Rust.

## Solving

Depth-first search with backtracking over the move space, emitting the
full move sequence on success. Board size 6 gets memory-hungry; size 5
solves from any starting position.

## Build

    cargo build --release
    ./target/release/peg_game <board_size> <empty_position>

Full writeup: [final.pdf](final.pdf)

---

*CSC 447 (Artificial Intelligence), Kutztown University, Fall 2021.
Archived. The flatten-the-structure move — 2D semantics over a 1D
array — is one I've reused ever since.*


