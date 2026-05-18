# CPU Inside-Out

An interactive, single-file CPU simulator built to demystify how processors actually work. Designed for high school students, curious beginners, and anyone who's ever wondered what really happens between writing code and seeing output.

Write assembly, hit step, and watch instructions flow through the fetch → decode → execute → writeback cycle in real time. Animated buses, glowing registers, plain-English explanations of every step.

![License: MIT](https://img.shields.io/badge/license-MIT-amber)
![No build step](https://img.shields.io/badge/build-none-green)
![Single file](https://img.shields.io/badge/files-1-cyan)

## What's inside

A complete simulated CPU with:

- **Program Counter, Instruction Register, Control Unit, ALU** — the actual functional blocks every CPU has
- **Four general-purpose registers** (R0–R3) plus Zero and Negative flags
- **Color-coded buses** — data (green), address (cyan), control (magenta) — that animate when active
- **A small but real assembly language** with 12 instructions covering arithmetic, comparison, conditional jumps, and I/O
- **Six pre-loaded example programs** from "add two numbers" up through factorial and Fibonacci
- **Adjustable execution speed** from frame-by-frame to fast playback
- **A plain-English execution log** that explains every micro-step as it happens

## How to use it

1. Open `index.html` in any modern browser. No install, no build step, no server.
2. Pick an example from the dropdown — start with **Simple addition**.
3. Press **▸ Step** to advance one phase at a time, or **▶ Run** to watch it play through.
4. Use the speed slider to slow things down when you want to actually see what's happening.
5. Edit the code directly — the program reloads automatically when you change it.

### Live demo

If you fork this repo and enable GitHub Pages (Settings → Pages → Deploy from `main` branch), your simulator will be live at `https://<your-username>.github.io/<repo-name>/`.

## The four phases of every instruction

Every single instruction the CPU runs goes through these four phases. The simulator highlights which one is active.

| Phase | What happens |
|-------|--------------|
| **① Fetch** | The Program Counter tells memory which instruction to send. Memory returns it into the Instruction Register. |
| **② Decode** | The Control Unit reads the instruction and figures out which circuits to activate. |
| **③ Execute** | The actual work happens — the ALU does math, registers move data, etc. |
| **④ Writeback** | Results are stored back into a register, the flags update, or the PC jumps. |

## Instruction reference

| Instruction | Meaning |
|-------------|---------|
| `MOV Rx, #n` | Load the immediate value `n` into register `Rx` |
| `MOV Rx, Ry` | Copy `Ry` into `Rx` |
| `ADD Rx, Ry` | `Rx = Rx + Ry` |
| `SUB Rx, Ry` | `Rx = Rx − Ry` |
| `MUL Rx, Ry` | `Rx = Rx × Ry` |
| `CMP Rx, Ry` | Compare `Rx` and `Ry` — sets the Z (zero) and N (negative) flags |
| `JMP label` | Always jump to `label` |
| `JZ label`  | Jump to `label` if the Zero flag is set (the values were equal) |
| `JNZ label` | Jump to `label` if the Zero flag is *not* set |
| `JG label`  | Jump to `label` if greater (Z=0 and N=0) |
| `OUT Rx`    | Print the value of `Rx` to the console |
| `HALT`      | Stop execution |

Labels are defined with a name followed by a colon, e.g. `loop:` on its own line. Comments start with `;`.

## Example: counting from 1 to 5

```asm
MOV R0, #1      ; counter
MOV R1, #5      ; limit
MOV R2, #1      ; step size

loop:
OUT R0          ; print current count
ADD R0, R2      ; counter += 1
CMP R0, R1      ; compare counter to limit
JG done         ; if counter > limit, exit
JMP loop        ; otherwise loop again

done:
HALT
```

## Teaching notes

A few moments worth pausing on when you walk a student through this:

- **The PC is just a counter.** Most of the time it adds 1 after each instruction. Jumps change it — and that's how *every* loop, if-statement, and function call in any language eventually works under the hood.
- **The ALU has no memory.** It takes two inputs, does math, returns one output. That's it. The "smart" part of the CPU is actually astonishingly dumb.
- **`CMP` doesn't store its result anywhere visible — it just sets flags.** That's why `CMP` is always followed by a conditional jump. The flags are how the CPU "remembers" a comparison just long enough to act on it.
- **Everything is movement.** The CPU is mostly a traffic system shuffling numbers between registers, memory, and the ALU. The math is the easy part.

## Stretch challenges

Once a student is comfortable with the examples, try:

- Print all even numbers from 2 to 20
- Compute 2⁸ using only `ADD`
- Check whether `R0` is greater than both `R1` and `R2`
- Compute the sum 1 + 2 + 3 + ... + 10
- Implement integer division (how many times does `R1` fit into `R0`?)

The four-register limit is itself a great lesson in what made early computing genuinely hard.

## License

MIT. Use it, fork it, remix it, teach with it.
